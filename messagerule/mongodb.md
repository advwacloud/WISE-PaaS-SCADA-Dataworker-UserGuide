# Message Rule - mongodb

---

依照使用者定義的Schema寫入MongoDB。

#### 欄位說明：

| Property | 類型 | Description |
| :--- | :--- | :--- |
| tableName | String | Collection 名稱 |
| index | Object | Collection 的 index \(請參考[Mongoose](https://mongoosejs.com/docs/guide.html)\) |
| schema | Object | Collection 的 schema \(請參考[Mongoose](https://mongoosejs.com/docs/guide.html)\) |
| mapping | Object | schema 與封包處理後的數據格式的對應表 |
| allMatch | Boolean | 是否要檢查mapping中的所有欄位都必須要存在於封包中才寫入資料庫 |

#### Sample:
MESSAGE_RULE:
```
{
  "name": "HistRawData",
  "type": "mongodb",
  "options": {
    "tableName": "m2i_RealTimeData",
    "index": [
      {
        "fields": {
          "s": 1,
          "d": 1,
          "ts": 1
        },
        "options": {
          "unique": false
        }
      },
      {
        "fields": {
          "s": 1,
          "d": 1,
          "ts": -1
        },
        "options": {
          "unique": false
        }
      },
      {
        "fields": {
          "d": 1,
          "ts": 1
        },
        "options": {
          "unique": false
        }
      },
      {
        "fields": {
          "d": 1,
          "ts": -1
        },
        "options": {
          "unique": false
        }
      },
      {
        "fields": {
          "d": 1
        },
        "options": {
          "unique": false
        }
      },
      {
        "fields": {
          "ts": -1
        },
        "options": {
          "unique": false
        }
      },
      {
        "fields": {
          "ts": 1
        },
        "options": {
          "unique": false
        }
      }
    ],
    "schema": {
      "s": {
        "type": "String"
      },
      "d": {
        "type": "String"
      },
      "ts": {
        "type": "Date",
        "default": "Date.now"
      }
    },
    "mapping": {
      "s": "$.scadaId",
      "d": "$.deviceId",
      "ts": "$.ts",
      "Status": "$..tags[?(@.name.match(/.*Status/i))].value",
      "IsAlarm": "$..tags[?(@.name.match(/.*IsAlarm/i))].value",
      "AlmCode": "$..tags[?(@.name.match(/.*AlmCode/i))].value",
      "AlmMsg": "$..tags[?(@.name.match(/.*AlmMsg/i))].value"
    },
    "allMatch": false
  }
}
```



