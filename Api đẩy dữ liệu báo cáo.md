## Mô tả cho api thêm chỉ tiêu cho các phần mềm

**Input**: 
```json
{
    "indicators": [
        {
            "code": "indicatorCode1",
            "value": 123,
            "unit": "Đơn vị tính 1"
        },
        {
            "code": "indicatorCode2",
            "value": 123,
            "unit": "Đơn vị tính 2"
        },
    ],
    "dataTypeId": 1,
    "year": 2020,
    "periodId": 1,
    "officeCode": "000-00-00-H40"
}
```
Trong đó:
`indicators`(`List<object>`): Danh sách chỉ tiêu và giá trị   
`dataTypeId`(`int`): Loại số liệu
|dataTypeId|Giá trị|
|---|---|
| 1 |Kế hoạch|
| 2 |Ước tính|
| 3 |Thực hiện|
| 4 |Chính thức|
`year`(`int`): Năm nhập liệu   
`periodId`(`int`): Kỳ nhập liệu
|periodId|Giá trị|
|---|---|
|1-12|tháng 1- tháng 12|
|13-16|quý 1 – quý 4|
|17|6 tháng đầu năm|
|18|6 tháng cuối năm|
|20|cả năm|
|21|5 năm|
`officeCode`(`string`): Mã đơn vị


**Output**:
```json
{
    "data": null,
    "total": 2,
    "error": {
        "userMessage": "",
        "internalMessage": "",
        "code": 200
    }
}
```