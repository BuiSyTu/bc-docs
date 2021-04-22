### [POST] `/_vti_bin/TD.QuanLyMaDinhDanh.Service/Mddservice.svc/LoginUser`

**Mô tả**: Lấy token đăng nhập

**Body**
```json
{
    "user": "demo1", // tên đăng nhập
    "pass": "Tandan@123" // mật khẩu
}
```

**Output**
```json
{
    "data": {
        "accessToken": {token},
        "expiresIn": "2021-01-09 14:39:18", // thời gian hết hạn
        "refreshToken": "1ibdg3xa.vqx",
        "tokenType": "Bearer"
    },
    "error": {
        "code": 200,
        "internalMessage": null,
        "userMessage": null
    }
}
```

<div style="page-break-after: always"></div>

### [GET]: `/_vti_bin/TD.WCF /WCFService.svc/GetUrlPublic`

**Mô tả**: Đăng nhập qua `{token}` và điều hướng sang trang `{urlRedirect}`

**Danh sách tham số**:

- `token`: Từ `accessToken` của phần api trước đó, encode base64 1 lần

- `urlRedirect`: Trang muốn điều hướng

**Ví du:**
- token: `1a2b3c`
- urlRedirect: `http://google.com`

**Gọi** `/_vti_bin/TD.BC.DW/DWService.svc/indicators/BCCP?token=1a2b3c&urlRedirect=http://google.com`

<div style="page-break-after: always"></div>

###[GET]: `/_vti_bin/TD.BC.DW/DWService.svc/indicators/BCCP`

**Mô tả**: Lấy danh sách chỉ tiêu báo cáo chính phủ

**Output**:
```json
{
    "data": List<Indicator>, // Danh sách chỉ tiêu
    "error": {
        "code": 200,
        "internalMessage": "",
        "userMessage": ""
    },
    "total": 2875
}
```

Trong đó:
```json
    Indicaror: {
        "code": "BCCP", // mã chỉ tiêu
        "childrens": List<Indicator>, // danh sách các chỉ tiêu con
        "id": 1, // id chỉ tiêu
        "name": "Chỉ tiêu 1.1", // tên chỉ tiêu
        "parentCode": "BCCP1" // mã chỉ tiêu cha

    }
```

<div style="page-break-after: always"></div>

### [GET]: `/_vti_bin/TD.BC.DW/DWService.svc/indicators`

**Mô tả**: Lấy giá trị nhập liệu

**Danh sách tham số**:
- `officeCode`: mã đơn vị
- `indicatorCode`: mã chỉ tiêu
- `dataTypeId`: Loại số liệu

|dataTypeId|Giá trị|
|---|---|
|1|Kế hoạch|
|2|Ước tính|
|3|Thực hiện|
|4|Chính thức|

- `periodId`: Kỳ nhập

|periodId|Giá trị|
|---|---|
|1-12|tháng 1- tháng 12|
|13-16|quý 1 – quý 4|
|17|6 tháng đầu năm|
|18|6 tháng cuối năm|
|20|cả năm|
|21|5 năm|

- `dataYear`: Năm nhập


**Output**:
```json
    {
        "data": IndicatorValue // object giá trị chi tiêu, mô tả ở bên dưới
        "error": {
            "code": 200,
            "internalMessage": "",
            "userMessage": ""
        },
        "total": 2875
    }
```

<div style="page-break-after: always"></div>

Trong đó:
```json
    IndicatorValue:
        {
            "indicatorCode": "abc", //mã chỉ tiêu.
            "unit": "tấn", // đơn vị tính
            "value": 123 // giá trị nhập liệu
        }
```

**Ví dụ** muốn lấy giá trị chỉ tiêu 
- có mã (indicatorCode) `BPC_KTXH_TDTTGRDP`
- của đơn vị UBND tỉnh Quảng Trị (officeCode = `000.00.00.H50`)
- với loại số liệu là chỉnh thức (dataType = `3`)
- năm nhập là 2019 (dataYear = `2019`)
- kỳ nhập liệu là cả năm (periodId = `20`)

Gọi: `/_vti_bin/TD.BC.DW/DWService.svc/indicators?officeCode=000.00.00.H50&indicatorCode=BPC_KTXH_TDTTGRDP&dataTypeId=3&periodId=20&dataYear=2019`

<div style="page-break-after: always"></div>

### [POST]: `/_vti_bin/TD.BC.DW/DWService.svc/indicators`

**Mô tả**: Lấy hàng loạt giá trị chỉ tiêu theo danh sách

**Body**:
```json
{
    "officeCode": "mã đơn vị", // string
    "indicatorCodes": ["abc", "def"], // danh sách các mã chỉ tiêu, List<string>
    "dataTypeId": 1, // loại số liệu, int
    "periodId": 1, // Kỳ nhập liệu, int
    "dataYear": 2019 // Năm nhập liệu
}
```
**Output**:
```json
    {
        "data": List<IndicatorValue> // danh sách IndicatorValue, mô tả xem phía trên
        "error": {
            "code": 200,
            "internalMessage": "",
            "userMessage": ""
        },
        "total": 2875
    }
```

<div style="page-break-after: always"></div>

### [GET]: `/vti_bin/TD.BC.DW/DWService.svc/offices`

**Mô tả**: Lấy danh sách đơn vị hệ thống

**Output**:
```json
    {
        "data": List<Office> // object thông tin đơn vị, mô tả ở bên dưới
        "error": {
            "code": 200,
            "internalMessage": "",
            "userMessage": ""
        },
        "total": 2875
    }
```

Trong đó:

```json
    Office: 
        {
            "Code": "Mã đơn vị",
            "Name": "Tên đơn vị"
        }
```

### [Get]: `/vti_bin/TD.BC.DW/DWService.svc/indicators/office/hasdata/{officeCode}`

**Mô tả**: Lấy tất cả những chỉ tiêu đơn vị có dữ liệu

**Output**:
```json
    {
        "data": List<IndicatorInformationShortCut> // object thông tin chi tiêu, mô tả ở bên dưới
        "error": {
            "code": 200,
            "internalMessage": "",
            "userMessage": ""
        },
        "total": 2875
    }
```

<div style="page-break-after: always"></div>

Trong đó:

```json
    IndicatorInformationShortCut: 
        {
            "code": "Mã chỉ tiêu",
            "name": "Tên chỉ tiêu"
        }
```

### [GET]: `/vti_bin/TD.BC.DW/DWService.svc/indicators/hasdata`

**Mô tả**: Lấy danh sách các chỉ tiêu có dữ liệu

**Danh sách tham số**:
- `officeCode`: Mã đơn vị
- `dataTypeId`: Id loại dữ liệu
- `periodId`: Id kỳ nhập dữ liệu
- `datayear`: năm nhập liệu

**Output**
```json
    {
        "data": List<IndicatorInformationShortCut> // object thông tin chi tiêu, mô tả ở bên dưới
        "error": {
            "code": 200,
            "internalMessage": "",
            "userMessage": ""
        },
        "total": 2875
    }
```

Trong đó:

```json
    IndicatorInformationShortCut: 
        {
            "code": "Mã chỉ tiêu",
            "name": "Tên chỉ tiêu"
        }
```
