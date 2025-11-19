Zabbix Monitoring Stack - Docker Compose

https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker
https://img.shields.io/badge/Zabbix-7.4.6-D50000?style=for-the-badge
https://img.shields.io/badge/PostgreSQL-17.6-336791?style=for-the-badge&logo=postgresql

Stack completo de monitoreo Zabbix implementado con Docker Compose para entornos de producción.
🏗️ Arquitectura del Stack
Componente Versión Descripción
PostgreSQL 17.6 Base de datos principal
Zabbix Server 7.4.6 Servidor de monitoreo central
Zabbix Web Interface 7.4.6 Dashboard web (Nginx + PHP-FPM)
Zabbix Agent2 7.4.3 Agente para monitoreo del host
SNMP Trap Receiver 7.4.6 Receptor de trampas SNMP
🔌 Esquema de Puertos
Puerto Protocolo Propósito
8080 TCP Interfaz web HTTP
4443 TCP Interfaz web HTTPS
10051 TCP Comunicación con agentes activos
162 UDP Recepción de trampas SNMP
💾 Volúmenes de Datos
Volumen Contenedor Propósito
zabbix-postgresdb PostgreSQL Base de datos Zabbix
zabbix-server Zabbix Server Configuración del servidor
zabbix-snmptraps Zabbix Server Trampas SNMP recibidas
zabbix_dashboard_config Zabbix Web Configuración del dashboard
zabbix_certificados Zabbix Web Certificados SSL/TLS
🚀 Implementación Rápida
Prerrequisitos

    Docker Engine 20.10+

    Docker Compose 2.0+

Configuración Inicial

    Clonar el repositorio:

bash

git clone <repository-url>
cd zabbix-stack

    Configurar variables de entorno:

bash

# Editar archivo .env

cp .env.example .env
nano .env

Variables de Entorno Requeridas
env

# CONFIGURACIÓN CRÍTICA - MODIFICAR OBLIGATORIAMENTE

POSTGRES_USER=zabbix_admin
POSTGRES_PASSWORD=your_secure_password_here

# CONFIGURACIÓN OPCIONAL

ZBX_SERVER_HOST=zabbix-server
ZBX_SERVER_NAME=Zabbix Monitoring
ZBX_TIMEZONE=America/Bogota

Despliegue
bash

# Iniciar stack completo

docker-compose up -d

# Verificar estado

docker-compose ps

# Consultar logs

docker-compose logs -f zabbix-server

🌐 Acceso al Sistema

Una vez desplegado, acceda a las interfaces:

    Interfaz Web HTTP: http://<SERVER_IP>:8080

    Interfaz Web HTTPS: https://<SERVER_IP>:4443 (requiere certificados válidos)

Configuración HTTPS

Para habilitar HTTPS con certificados válidos:
bash

# Copiar certificados al directorio designado

cp ssl/cert.pem ssl/key.pem ./certificates/

# Reiniciar servicio web

docker-compose restart zabbix-web

🔧 Configuración de Agentes

El stack incluye Zabbix Agent2 configurado para monitoreo del host local. Para monitoreo remoto:
bash

# Ejemplo: conectar agente remoto

ZabbixServer=<SERVER_IP>
ZabbixServerActive=<SERVER_IP>

📊 Monitoreo SNMP

El receptor de trampas SNMP está configurado en el puerto UDP 162. Para dispositivos SNMP:
snmp

# Configuración ejemplo para dispositivo SNMP

snmp-server host <ZABBIX_SERVER_IP> traps version 2c public

🛠️ Comandos de Administración
bash

# Estado de servicios

docker-compose ps

# Logs en tiempo real

docker-compose logs -f

# Backup de base de datos

docker-compose exec postgres pg_dump -U $POSTGRES_USER zabbix > backup.sql

# Reinicio selectivo

docker-compose restart zabbix-server

# Apagar stack

docker-compose down

🔒 Consideraciones de Seguridad

    Cambiar credenciales por defecto inmediatamente después del despliegue

    Configurar firewall para restringir acceso a puertos expuestos

    Utilizar certificados SSL válidos para producción

    Monitorear logs de acceso regularmente

📝 Notas de Versión

    Zabbix 7.4.6: Última versión LTS con soporte extendido

    PostgreSQL 17.6: Optimizado para cargas de trabajo de monitoreo

    Zabbix Agent2: Soporte nativo para contenedores y orquestación
