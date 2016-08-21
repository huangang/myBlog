title: 自动化 Nginx 反向代理 Docker容器
date: 2016-01-20 16:11:34 
tags: [nginx,docker]
---
# 下载安装[docker-gen](https://github.com/jwilder/docker-gen)
``` bash
wget https://github.com/jwilder/docker-gen/releases/download/0.5.0/docker-gen-linux-amd64-0.5.0.tar.gz
tar xvzf docker-gen-linux-amd64-0.5.0.tar.gz
chmod +x docker-gen
mv docker-gen /usr/bin/
```
<!-- more -->
## nginx.tmpl
这个例子 Nginx 模板可以被用于生成一个 Docker 容器使用虚拟主机路由的反向代理配置文件。
这个模板是使用 golang text/template package 实现的。它使用一个通用的 groupBy 模板函数通过它们的 VIRTUAL_HOST 环境变量来分组运行的容器。
这简化了遍历容器来生成一个负载均衡后端以及使得零停机部署可行。

```
{{ range $host, $containers := groupBy $ "Env.VIRTUAL_HOST" }}
upstream {{ $host }} {

{{ range $index, $value := $containers }}
    {{ with $address := index $value.Addresses 0 }}
    server {{ $address.IP }}:{{ $address.Port }};
    {{ end }}
{{ end }}

}

server {
    #ssl_certificate /etc/nginx/certs/demo.pem;
    #ssl_certificate_key /etc/nginx/certs/demo.key;

    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;

    server_name {{ $host }};

    location / {
        proxy_pass http://{{ $host }};
        include /etc/nginx/proxy_params;
    }
}
{{ end }}
```

放到 `/etc/nginx/`目录下面
创建sites-enabled:`mkdir /etc/nginx/sites-enabled/`
修改`/etc/nginx/nginx.conf` 在http最下面加入一行 `include /etc/nginx/sites-enabled/default;`
运行docker容器的时候需要有VIRTUAL_HOST环境变量启动,如:`docker run -i -t -d -P -e VIRTUAL_HOST=next.your.com yourImage/version:tag `
最后运行docker-gen
`docker-gen -only-exposed -watch -notify "/etc/init.d/nginx reload" /etc/nginx/nginx.tmpl /etc/nginx/sites-enabled/default`
`-only-exposed` - 仅仅使用容器已经暴露的端口。
`-watch` - 启动之后，监控 docker 容器事件和重新生成模板。
`-notify "/etc/init.d/nginx reload"` - 在模板生成后重载 nginx 配置。
`/etc/nginx/nginx.tmpl` - nginx 模板。
`/etc/nginx/sites-enabled/default` - 目标文件。

如果`/etc/nginx/proxy_params`不存在,可以手动编辑生成
`vim /etc/nginx/proxy_params`,写入以下内容
```
proxy_set_header Host              $host;
proxy_set_header X-Real-IP         $remote_addr;
proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
```
在重新运行`docker-gen`