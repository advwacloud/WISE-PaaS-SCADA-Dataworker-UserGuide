# Message Rule - transfer

---

將收到的資料封包轉成使用者定義的格式後再轉傳出去。

#### 欄位說明：

| Property | Description |
| :--- | :--- |
| protocol | 透過何種Protocol轉傳, 目前支援: "amqp" |
| topic | 轉傳的目標Topic, 適用於"amqp"和"mqtt" |
| format | 定義處理後的封包格式. horizontal: true/false 是否要將所有測點轉成單一階層水平格式. fields: 封包格式中指定的欄位 |
| hasAllTags | 檢查hasAllTags中的所有測點都必須要存在於封包中才執行轉傳 |

Sample:

```
MESSAGE_RULE: {
  name: 'APM_OEE',
  type: 'transfer',
  options: {
    protocol: 'amqp',
    topic: 'apm.scada.{spaceId}.workorder',
    format: {
      horizontal: true,
      fields: {
        scadaID: '$.scadaId',
        devID: '$.deviceId'
      }
    },
    hasAllTags: ['woType', 'woID']
  }
}
```



