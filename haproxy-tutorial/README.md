# 步驟

在本機執行

先 build

```cmd
docker build -t my-haproxy .
```

RUN

```cmd
docker run -p 8080:80  my-haproxy
```

瀏覽 [http://0.0.0.0:8080/](http://0.0.0.0:8080/)

```cmd
apt-get update
apt-get install haproxy
apt-get install rsyslog
```

寫 log

```cmd
logger "test"
```

> /var/log tail -F syslog

會輸出 log 資訊