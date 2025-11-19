# Zabbix Stack with Docker Compose

Monitoreo con Zabbix Server, Web, Postgres, SNMP y Agente2 para monitoreo del localhost.

## Componentes

- Postgres 17.6
- Zabbix Server 7.4.6
- Zabbix Dashboard 7.4.6 (Nginx)
- Zabbix Agent2 7.4.3 (Ubuntu)
- SNMP Trap Receiver

## Puertos

- 8080:Http
- 4443:Https
- 10051:TCP (Agentes activos)
- 162:UDP (SNMP Traps)

## Volumenes

- zabbix-postgresdb: Base de datos de Zabbix
- zabbix-server: Datos de configuración del servidor de Zabbix
- zabbix-snmptraps: Notificaciones de dispositivos SNMP
- zabbix_dashboard_config: Datos de configuración del dashboard de Zabbix
- zabbix_certificados: Certificados para HTTPS

## Como usar

1-) Descargar el directorio Actual
2-) Cambiar los valores de la variables estrictamente necesarias en .env

POSTGRES_USER=<USUARIO BD>
POSTGRES_PASSWORD=<CONTRASEÑA BD>

3-) Cambiar los valores de la variables opcionales en .env (Direccionamineto IP, nombre de contenedores, TimeZone, puertos de escucha, entre otros)

4-) Ejecute desde el directorio actual

docker-compose up -d

5-) Una vez se levanta el stack de Zabbix este es accesible desde

- http://IP_SERVIDOR_LOCAL:8080
- https://IP_SERVIDOR_LOCAL:4443 (Si se copiaron certificados validos en /etc/ssl/nginx del Zabbix Dashboard)
