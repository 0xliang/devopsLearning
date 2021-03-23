### How to use zabbix and zabbix-agent in Docker way

**ENV**
- CentOS7
- Docker version: 18.06.3-ce
- image: zabbix/zabbix-agent, zabbix/zabbix-appliance:latest
- date: 2021.03.23
- Author: 0xliang

**describe**: It is easy to use docker to build zabbix Server, and zabbix-agent, just record what I had operate

**STEP**
1. Install Docker in CentOS7(not mention here)
2. ```(install Server) docker run --name zabbix 8080:80 -p 10051:10051 -d zabbix/zabbix-appliance:centos-4.0.18```
3. ```(install agent) docker run --name zabbixAgent -e ZBX_HOSTNAME="forZabbixServerFound" -p 10050:10050 -e ZBX_SERVER_HOST="zabbixServer"  -d zabbix/zabbix-agent```
4. open ip:8080 in web browser, and operate it

*note: if your zabbix server and agent in the same mechine, the agent's "ZBX_SERVER_HOST" addres IP must be the docker IP(like 172.17.0.2), it is not work if you use the host(centos7) IP or loop(127.0.0.1) ip, I don't really understand why*