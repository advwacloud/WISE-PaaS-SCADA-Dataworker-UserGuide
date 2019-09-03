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

#### 欄位說明：

| Property | Description |
| :--- | :--- |
| name | Rule 名稱 |
| type | Message Rule 類型 |
| events | Message Rule 事件定義 (請參考以下關於欄位事件說明) |
| options | 各類型自定義的屬性 \(請參考各類型的說明\) |


#### 欄位事件說明：
| Event | Description |
| :--- | :--- |
| onMatched | 當message符合定義的Rule時觸發<br>- rawdata: 是否紀錄到歷史資料 (true/false, 預設為true) |
| onNotMatched | 當message不符合定義的Rule時觸發<br>- rawdata: 是否紀錄到歷史資料 (true/false, 預設為true) |

#### 範例：

```
{
    name: 'XXX',
    type: 'transfer',
    events: {
      onMatched: {
        rawdata: true // 當符合Rule時紀錄歷史資料
      },
      onNotMatched: {
        rawdata: false // 當不符合Rule時不紀錄歷史資料
      }
    },
    options: {
      ...
    }
}
```