### Chung
`BaseUrl`: `https://api.quangbinh.gov.vn/bc`  
`Authorization`: `Bear 780881a5-e60e-32c9-92a6-a9e5b961a5a5`

### [GET]: `/indicators`

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

<div style="page-break-after: always"></div>

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

Gọi: `/indicators?officeCode=000.00.00.H50&indicatorCode=BPC_KTXH_TDTTGRDP&dataTypeId=3&periodId=20&dataYear=2019`

<div style="page-break-after: always"></div>

### [POST]: `/indicators`

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

Trong đó:

```json
    IndicatorValue: 
        {
            "indicatorCode": "Mã chỉ tiêu",
            "unit": "Đơn vị tính",
            "value": "Giá trị"
        }
```



<div style="page-break-after: always"></div>

### [GET]: `/offices`

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

<div style="page-break-after: always"></div>

### [Get]: `/indicators/office/hasdata/{officeCode}`

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

Trong đó:

```json
    IndicatorInformationShortCut: 
        {
            "code": "Mã chỉ tiêu",
            "name": "Tên chỉ tiêu"
        }
```

<div style="page-break-after: always"></div>

### [GET]: `/indicators/hasdata`

**Mô tả**: Lấy danh sách các chỉ tiêu có dữ liệu và được lọc theo các tham số dưới đây

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

**Ví dụ**: Muốn lấy các chỉ tiêu
- Mã đơn vị là 000.00.00.H50
- Kỳ nhập liệu là cả năm
- Năm nhập liệu là 2019
- Loại dữ liệu bất kỳ (dataTypeId bỏ trống)

Gọi: `/indicators/hasdata?officeCode=000.00.00.H50&periodId=20&dataYear=2019`
