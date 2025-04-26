# Java

## Deploy


SFTP client  

https://winscp.net/eng/download.php

SSH  

```
ssh usuario@ip-del-servidor -p puerto

ssh root@192.168.1.100 -p 22
```

Listar usuarios

```
cat /etc/passwd
```

Crear usuario

```
sudo adduser --system --no-create-home --group java-app-user
```

Permisos

```
sudo chown -R java-app-user:java-app-user /opt/java/java-app.jar

sudo chmod 750 /opt/java/java-app.jar
```

Servicio

```
sudo nano /etc/systemd/system/java-app.service
```

```
[unit]
Description=Servicio java-app
After=syslog.target network.target

[Service]
User=java-app-user
WorkingDirectory=/opt/java
ExecStart=/usr/bin/java -jar /opt/java/java-app.jar
SuccessExitStatus=143
Restart=on-failure  #always
RestartSec=5
Environment="JAVA_OPTS=-Xms256m -Xmx512m"

[Install]
WantedBy=multi-user.target
```

Recargar la lista de servicios

```
sudo systemctl daemon-reload
```

Habilitar / Deshabilitar inicio automático del servicio
```
sudo systemctl enable java-app.service

sudo systemctl disable java-app.service
```

Manejar servicio

```
sudo systemctl status java-app.service

sudo systemctl start java-app.service

sudo systemctl stop java-app.service
```

Mostrar procesos

```
sudo ps aux | grep java
```

Detener procesos (reemplaza PID con el número que aparezca)

```
sudo kill -9 PID
```

Listar servicios

```
systemctl --user list-units --type=service
systemctl list-units --type=service | grep running
service --status-all
```
















