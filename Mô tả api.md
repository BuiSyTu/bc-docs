## Mô tả cho api lấy giá trị chỉ tiêu

**Input**: 
```json
{
    "indicatorCodes": ["indicatorCode1", "indicatorCode2"],
    "dataTypeId": 1,
    "year": 2020,
    "periodId": 1,
    "officeCode": "000-00-00-H40"
}
```
Trong đó:  
- `indicatorCodes` (`List<string>`): Danh sách mã chỉ tiêu  
- `dataTypeId` (`int`): Loại số liệu  


|dataTypeId|Giá trị|
|---|---|
|1|Kế hoạch|
|2|Ước tính|
|3|Thực hiện|
|4|Chính thức|
- `year` (`int`): Năm nhập liệu  
- `periodId` (`int`): Kỳ nhập liệu  

|periodId|Giá trị|
|---|---|
|1-12|tháng 1- tháng 12|
|13-16|quý 1 – quý 4|
|17|6 tháng đầu năm|
|18|6 tháng cuối năm|
|20|cả năm|
|21|5 năm|
- `officeCode` (`string`): Mã đơn vị  

<div style="page-break-after: always"></div>

**Output**:
```json
{
    "data":
    [
        {
            "indicatorCode": "indicatorCode1",
            "value": "1234",
            "unit": "kg"
        },
        {
            "indicatorCode": "indicatorCode2",
            "value": "12",
            "unit": "tấn"
        }
    ]
}
```
Trong đó:  
- `indicatorCode` (`string`): Mã chỉ tiêu  
- `value` (`string`): Giá trị nhập liệu  
- `unit` (`string`): Đơn vị tính  