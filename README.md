# DataX-redis-writer

------------


## 1 支持功能

* 导入数据到redis（默认）

* 根据数据源删除redis key

* 根据数据源删除hash类型的field

## 2 支持数据类型

* string
```json
{
  "name": "rediswriter",
  "parameter": {
    "redisMode": "cluster",
    "address": "xxxxxxxxxxxxx:6379,xxxxxxxxxxxxx:6479,xxxxxxxxxxxxx:6379,xxxxxxxxxxxxx:6479,xxxxxxxxxxxxx:6379,xxxxxxxxxxxxx:6479",
    "auth": "Pye9WQAYsgetVrLw",
    "writeType": "string",
    "config": {
      "colKey": {
        "name": "uid",
        "index": 0
      },
      "colValue": {
        "name": "name",
        "index": 2
      },
      "expire": 300,
      "keyPrefix": "datax:string:"
    }
  }
}
```
* list
```json
{
  "name": "rediswriter",
  "parameter": {
    "redisMode": "cluster",
    "address": "xxxxxxxx:6379,xxxxxxxx:6479,xxxxxxxx:6379,xxxxxxxx:6479,xxxxxxxx:6379,xxxxxxxx:6479",
    "auth": "xxxxxxxx",
    "writeType": "list",
    "config": {
      "colKey": {
        "name": "uid",
        "index": 0
      },
      "colValue": {
        "name": "channels",
        "index": 1
      },
      "valueDelimiter": ",",
      "pushType": "overwrite",
      "expire": 300,
      "keyPrefix": "datax:list:"
    }
  }
}
```

* hash
```json
{
  "name": "rediswriter",
  "parameter": {
    "redisMode": "cluster",
    "address": "xxxxxx:6379,xxxxxx:6479,xxxxxx:6379,xxxxxx:6479,xxxxxx:6379,xxxxxx:6479",
    "auth": "Pye9WQAYsgetVrLw",
    "writeType": "hash",
    "config": {
      "colKey": {
        "name": "uid",
        "index": 0
      },
      "colValue": [
        {
          "name": "channels",
          "index": 1
        },
        {
          "name": "name",
          "index": 2
        }
      ],
      "valueDelimiter": ",",
      "expire": 300,
      "keyPrefix": "datax:hash:"
    }
  }
}
```


备注:
* delete
```json
{
  "name": "rediswriter",
  "parameter": {
    "redisMode": "cluster",
    "address": "xxxxxxx:6379,xxxxxxx:6479,xxxxxxx:6379,xxxxxxx:6479,xxxxxxx:6379,xxxxxxx:6479",
    "auth": "xxxxxxx",
    "writeType": "string",
    "writeMode": "delete",
    "config": {
      "colKey": {
        "name": "uid",
        "index": 0
      },
      "keyPrefix": "datax:"
    }
  }
}
```

## 3 参数说明
以下参数为datax自定义的json文件的parameter key下面的的参数

|一级参数|二级参数|三级参数|释义|备注|
|:--------:|:--------:|:--------:|--------|--------|
|redisMode|-|-|redis的部署模式，支持集群模式和单机模式，值：cluster或singleton|必需|
|address|-|-|redis的地址，单机模式：host:port，集群模式：host1:port1,host2:port2,|必需|
|auth|-|-|redis密码，没有则不加这个参数|非必需，有则填|
|ssl|-|-|ssl，默认false|非必需，默认false|
|db|-|-|redis db，默认0|非必需，默认0|
|writeType|-|-|写入redis的数据类型：string、list、hash|必需|
|writeMode|-|-|写入的模式，默认是写数据，设为delete是删数据|非必需可选，默认insert|
|config|-|-|以下二级参数的具体配置，配置三种redis数据类型|必需|
|-|strKey|-|(公共参数)自定义的redis key值，不通过数据源来定|非必需，strKey和colKey二选一|
|-|colKey|-|(公共参数)对应数据源的column，作为redis的key|非必需，strKey和colKey二选一|
|-|expire|-|(公共参数)redis key的过期时间，单位秒|非必需|
|-|batchSize|-|(公共参数)pipline批量每次导入redis的的大小|非必需|
|-|keyPrefix|-|(公共参数)redis key值的自定义前缀|非必需|
|-|keySuffix|-|(公共参数)redis key值的自定义后缀|非必需|
|-|colValue|-|(公共参数)redis value值对应的数据源列配置|除writeMode为delete时必需|
|-|-|name|(公共参数)对应的数据源列名|必需| 
|-|-|index|(公共参数)对应的数据源列索引|必需|
|-|valueDelimiter|-|(redis list类型参数)对应数据源column值的分隔符,只支持string类型的数据源column|writeType为list时必需|
|-|pushType|-|(redis list类型参数)list类型的push类型，有lpush，rpush，overwrite，默认overwrite|非必需，可选|
|-|hashFields|-|(redis hash类型参数)hash类型要删除的field，逗号隔开，次参数只对删除hash类型的field时有效|删除hash类型field时必需|

## 4 约束限制

略

## 5 FAQ

略

