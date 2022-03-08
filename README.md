# zabbix监控
## 使用方法
```bash
git clone --depth=1 https://github.com/danxiaonuo/zabbix.git
cd zabbix
docker-compose up -d
chmod -R 777 zbx_env
```
## 镜像加速
```bash
vi /etc/docker/daemon.json
"registry-mirrors":[
          "https://docker.xiaonuo.live"
    ]
```
### 更新页面集群信息
```bash
export HOST=$(docker exec -it mysql-server mysql -h 127.0.0.1 -u root -p'root_pwd' zabbix_server -sNe "select address from ha_node where status=3;" 2>/dev/null | grep -v 'mysql')
export PORT=$(docker exec -it mysql-server mysql -h 127.0.0.1 -u root -p'root_pwd' zabbix_server -sNe "select port from ha_node where status=3;" 2>/dev/null | grep -v 'mysql')
sed -i -e "s#ZBX_SERVER_HOST=.*#ZBX_SERVER_HOST=$HOST#g" -e "s#ZBX_SERVER_PORT=.*#ZBX_SERVER_PORT=$PORT#g" .env_vars/.env_web
docker-compose up -d
```
