# zabbix监控
## 使用方法
```bash
git clone --depth=1 https://github.com/danxiaonuo/zabbix.git
cd zabbix
docker-compose up -d
```
## 镜像加速
```bash
vi /etc/docker/daemon.json
"registry-mirrors":[
          "https://docker.xiaonuo.live"
    ]
```