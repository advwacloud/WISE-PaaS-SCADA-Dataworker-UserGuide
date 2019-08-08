# Message Rule

---

使用者可以自定義接收到封包後的Action。

#### 支援類型

* 資料庫
  * MongoDB
* 轉傳封包
  * AMQP

#### 封包處理技術

* [JsonPath](http://goessner.net/articles/JsonPath/)

#### 封包處理後的數據格式

```
{
  "scadaId": "cda43195-7a0a-4903-a533-d333d8c5f9d9",
  "deviceId": "Device1",
  "tags": [
    {
      "name": "Temp1",
      "value": 10.58
    },
    {
      "name": "Temp2",
      "value": 9.25
    }
  ],
  "ts": "2017-09-05T11:12:00+08:00"
}
```

#### 

#### 欄位說明：

| Property | Description |
| :--- | :--- |
| name | Rule 名稱 |
| type | Message Rule 類型 |
| options | 各類型自定義的屬性 \(請參考各類型的說明\) |



