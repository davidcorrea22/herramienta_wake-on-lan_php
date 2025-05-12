# Herramienta Wake-on-LAN + PHP + Python
Esta herramienta permite encender equipos de forma remota utilizando el protocolo Wake-on-LAN, combinado con un panel de control PHP y un servicio de envío de paquetes mágicos en Python.

# Componentes
- Panel Web (PHP + Apache): Accesible desde cualquier navegador por el puerto 80. Permite administrar equipos, programación de encendido automático de equipos y usuarios.
- API WOL (Python + Flask + Gunicorn): Servicio en el puerto 4000 encargado de enviar "magic packets".
- Base de datos (MySQL): Almacena todos los datos de la herramienta.

# Requisitos
- Instalar Docker Desktop e iniciar sus servicios: https://www.docker.com/products/docker-desktop
- Al menos dos equipos conectados por red Ethernet (no funciona en máquinas virtuales). Uno como servidor y otro como cliente:
    - Al menos un cliente: No necesitan ninguna instalación.
    - El cliente debe estar configurado para recibir paquetes mágicos: https://www.xataka.com/basics/wake-on-lan-que-como-configurarlo-windows-10

# Instalación
- Habilite el puerto 80 en el equipo servidor. Para esto, puede usar este comando: 
```bash
netsh advfirewall firewall add rule name="Abrir puerto 80" dir=in action=allow protocol=TCP localport=80
```

- Descargue el código fuente: 
```bash
git clone https://github.com/davidcorrea22/herramienta_wake-on-lan_php.git
```

- ⚠ EN DOCKER-COMPOSE.YML. CAMBIE EL VALOR DE "BROADCAST_IP". ESPECIFIQUE AHÍ LA DIRECCIÓN BROADCAST DE SU RED. ⚠

- Abra una terminal CMD, dirigase a C:\PROYECTO_WOL y levante los contenedores usando:
```bash
docker compose up -d --build
```

- Acceda al panel de control:
	- Desde http://localhost o http://{ip_del_equipo_servidor}
	- Los credenciales iniciales son: Usuario=administrador / Contraseña=administrador
	- Por motivos de seguridad, se recomienda eliminar este usuario después de crear uno nuevo.

# Carácteristicas
- Accesible desde dispositivos móviles.
- Gestión de dispositivos: Se pueden añadir, borrar y editar equipos informáticos.
- Comprueba si los equipos de la base de datos están encendidos o apagados.
- Encendido manual: Se puede elegir entre el botón "Encender" para un solo equipo o "Encender Todos" para un encendido global.
- Programación de encendido: Define los días de la semana y la hora a la que se encenderán todos los equipos automaticamente.
- Gestión de usuarios: Se pueden añadir, borrar y editar usuarios. Estos usuarios pueden ser administradores o usuarios estándar.
- Sistema de logs accesible desde Docker Desktop.

```yaml
services:
  db:
    image: mysql:9.2
    restart: always
    ports:
      - "3307:3306"
    environment:
      MYSQL_DATABASE: equipos
      MYSQL_USER: user
      MYSQL_PASSWORD: userpassword
      MYSQL_ROOT_PASSWORD: rootpassword
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - mynetwork
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "127.0.0.1", "-u", "user", "-puserpassword"]
      interval: 10s
      retries: 5
      start_period: 20s
      timeout: 5s
  wol:
    build: ./wakeonlan
    image: davidcorrea22/herramienta_wake-on-lan_php:wol
    restart: always
    ports:
      - "4000:4000"
    environment:
      - BROADCAST_IP=192.168.25.255
    networks:
      - mynetwork
    volumes:
      - ./wakeonlan:/app
  php:
    build: ./php
    image: davidcorrea22/herramienta_wake-on-lan_php:php
    restart: always
    ports:
      - "80:80"
    depends_on:
      db:
        condition: service_healthy
    networks:
      - mynetwork
    volumes:
      - ./php:/var/www/html
networks:
  mynetwork:
volumes:
  db_data:
```

# Advertencias
- Si reinicias el servidor, vuelva a levantar los contenedores para que la programación automática funcione de nuevo.
- La programación automática usa el horario Madrid/España.
- Los logs se pueden comprobar desde Docker Dekstop o usando:
```bash
  docker-compose logs 
```
