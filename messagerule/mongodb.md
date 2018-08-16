# Message Rule - MongoDB

---

依照使用者定義的Schema寫入MongoDB。



Sample:

```
MESSAGE_RULE:
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



