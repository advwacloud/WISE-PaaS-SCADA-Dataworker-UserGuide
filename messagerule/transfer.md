# Message Rule - transfer

---

將收到的資料封包轉成使用者定義的格式後再轉傳出去。

#### 欄位說明：

| Property | 類型 | Description |
| :--- | :--- | :--- |
| protocol | String | 透過何種Protocol轉傳, 目前支援: "amqp" |
| topic | String | 轉傳的目標Topic, 適用於"amqp"和"mqtt". <br>目前支援的變數: {spaceId} |
| format | Object | 定義處理後的封包格式. <br>horizontal: true/false 是否要將所有測點轉成單一階層水平格式. <br>fields: 封包格式中指定的欄位以及其對應的JsonPath |
| hasAllTags | Array | 檢查hasAllTags中的所有測點都必須要存在於封包中才執行轉傳 |

#### Sample:

MESSAGE_RULE:
```
{
  "name": "APM_OEE",
  "type": "transfer",
  "options": {
    "protocol": "amqp",
    "topic": "apm.scada.{spaceId}.workorder",
    "format": {
      "horizontal": true,
      "fields": {
        "scadaID": "$.scadaId",
        "devID": "$.deviceId"
      }
    },
    "hasAllTags": ["woType", "woID"]
  }
}

```
before:
```
topic: "/wisepaas/scada/92c51ca9-565a-4e52-b753-4b1e3a6ab99b/data"

payload: {
  "d": {
    "Device1": {
      "woType": "product",
      "woID": "21063157",
      "partNumber": "606-03-032KM",
      "prodName": "滑座（六鑫）（ＭＥ類）",
      "qty": 5,
      "woStatus": "O.K.",
      "startTime": "2018-10-15T08:08:08.976+08:00",
      "endTime": "2018-10-15T13:34:42.277+08:00",
      "description": "工程四(精修襯墊面)",
      "operatorName": "林育廷",
      "operatorId": "A-00001",
      "routing": "0090",
      "subRouting": "0040",
      "stdTS": 32,
      "stdTP": 35,
      "sdWorkTime": 195,
      "goods": 5,
      "defect": 0,
      "totalTS": 16020,
      "tpTime": "2018-10-15T08:08:08.976+08:00",
      "actWorkTime": 16020,
      "actTP": 30,
      "woProgress": 30.3
    }
  },
  "ts": "2019-01-01T10:19:51+08:00"
}
```
after:
```
topic: "apm/scada/1214f089-26c5-422b-b4a3-5c21f865fd1e/workorder"

payload: {
  "woType": "product",
  "woID": "21063157",
  "partNumber": "606-03-032KM",
  "prodName": "滑座（六鑫）（ＭＥ類）",
  "qty": 5,
  "woStatus": "O.K.",
  "startTime": "2018-10-15T08:08:08.976+08:00",
  "endTime": "2018-10-15T13:34:42.277+08:00",
  "description": "工程四(精修襯墊面)",
  "operatorName": "林育廷",
  "operatorId": "A-00001",
  "routing": "0090",
  "subRouting": "0040",
  "stdTS": 32,
  "stdTP": 35,
  "sdWorkTime": 195,
  "goods": 5,
  "defect": 0,
  "totalTS": 16020,
  "tpTime": "2018-10-15T08:08:08.976+08:00",
  "actWorkTime": 16020,
  "actTP": 30,
  "woProgress": 30.3,
  "scadaID": "92c51ca9-565a-4e52-b753-4b1e3a6ab99b",
  "devID": "Device1"
}
```



