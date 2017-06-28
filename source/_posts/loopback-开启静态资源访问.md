title: loopback 开启静态资源访问
date: 2017-06-28 10:56:30
tags: [loopback,nodejs,node]
---

在`server/middleware.json`的 `files`改成
``` json
 "files": {
    "loopback#static": {
      "params": "$!../client"
    }
  }
```
