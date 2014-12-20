deploy.go
=========

https://github.com/andrerocker/deploy.go

### Description

- Read a YAML and export this as a 'Command as a Service' :p


##### Example

Based on a simple yaml
```yaml
daemon:
  bind: 127.0.0.1
  port: 8888

commands:
  process:
    - get: ps -ef | grep {process}
      put: kill {process}
      delete: kill -9 {process}

  log:
    - get: tail -f {log}
```

You can do this
```console
$ curl http://server:8888/process/ruby
andrero+ 1337 45   5  11:18 pts/25   00:00:01 ruby bin/rails s
andrero+ 1338 45   29 11:18 pts/26   00:00:01 ruby bin/rails c

$ curl -X PUT http://server:8888/process/1338
$

$ curl http://server:8888/process/ruby
andrero+ 1337 45   5  11:18 pts/25   00:00:01 ruby bin/rails s
```

```console
$ curl http://server:8888/log/log/development.log
Started GET "/document/45" for 127.0.0.1 at 2014-11-30 03:20:32 -0200
Processing by DocumentController#show as HTML
  Parameters: {"id"=>"45"}
  User Load (0.4ms)  SELECT  "users".* FROM "users"  WHERE "users"."id" = 1337
  Doc Load (0.6ms)  SELECT  "docs".* FROM "docs"  WHERE "docs"."id" = 45 LIMIT 1
  Rendered document/show.html.erb within layouts/application (0.2ms)
Completed 200 OK in 97ms (Views: 94.6ms | ActiveRecord: 1.0ms)
```


