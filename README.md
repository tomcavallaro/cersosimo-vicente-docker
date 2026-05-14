# TP Docker — MySQL + Java App Server
## Datos del alumno
- Nombre: Cersosimo Vicente
## 1. ¿Qué es Docker?
Docker es una plataforma de contenedores que permite empaquetar aplicaciones junto con todas sus dependencias en unidades llamadas contenedores. Estos contenedores son ligeros, portables y se ejecutan de forma aislada, compartiendo el kernel del sistema operativo del host. A diferencia de las máquinas virtuales, son más rápidos y eficientes, lo que facilita el desarrollo, pruebas y despliegue de aplicaciones en distintos entornos sin problemas de compatibilidad.
## 2. Volúmenes en Docker
Los volúmenes en Docker son el mecanismo principal para persistir datos fuera del ciclo de vida de un contenedor. Esto significa que la información no se pierde aunque el contenedor se elimine o se vuelva a crear.
Se utilizan principalmente en bases de datos como MySQL para almacenar información de forma segura. Existen volúmenes nombrados, bind mounts y tmpfs, siendo los nombrados los más recomendados para entornos empresariales por su rendimiento y facilidad de gestión.
## 3. Redes en Docker
Las redes en Docker permiten la comunicación entre contenedores dentro de un mismo entorno. En una red bridge personalizada, los contenedores pueden comunicarse entre sí usando sus nombres como hostname gracias a la resolución DNS interna de Docker.
Esto permite que servicios como Payara Server se conecten a MySQL sin usar IPs fijas, solo utilizando el nombre del contenedor. Además, las redes mejoran la organización, el aislamiento y la seguridad del sistema.
## 4. ¿Por qué Payara Server?
Payara Server es un servidor de aplicaciones basado en Jakarta EE, ideal para entornos empresariales Java. Se elige porque ofrece soporte completo para tecnologías como JPA, EJB, CDI, JAX-RS y JMS.
Además, incluye una consola de administración web (GUI) accesible desde el puerto 4848, lo que facilita la gestión del servidor. También cuenta con imágenes Docker oficiales, buen rendimiento y escalabilidad desde desarrollo hasta producción sin cambiar el stack tecnológico.
## 5. Explicación del docker-compose.yml
El archivo docker-compose.yml permite definir y ejecutar múltiples contenedores de forma automatizada y centralizada.
En este proyecto se utiliza para levantar dos servicios principales: MySQL y Payara Server. Incluye la configuración de redes, volúmenes, puertos, variables de entorno y dependencias entre servicios.
## 6. Explicación del init.sql
El archivo init.sql es un script SQL que se ejecuta automáticamente al iniciar el contenedor de MySQL por primera vez. Su función es preparar la base de datos de forma automática.
Permite crear bases de datos, tablas e insertar datos iniciales sin intervención manual. Esto garantiza que todos los entornos tengan la misma estructura de base de datos desde el inicio, facilitando la reproducibilidad del sistema.
## 7. Dificultades y soluciones
Uno de los problemas más comunes en Docker es la conexión entre contenedores, que se soluciona usando redes bridge personalizadas y nombres de servicio en lugar de IPs o localhost.
Otro problema frecuente es la pérdida de datos al eliminar contenedores, lo cual se resuelve utilizando volúmenes persistentes.
También pueden surgir conflictos de puertos cuando varios servicios usan el mismo puerto, lo que se soluciona cambiando el mapeo en docker-compose.yml.

# Capturas de Pantalla Obligatorias

## **Parte 1 — Infraestructura Docker (5 capturas)**

## 1. Salida de docker --version y docker info en la terminal
<img width="279" height="53" alt="image" src="https://github.com/user-attachments/assets/49113f2d-26d5-40c8-bbc2-92eb36505228" />
## 2. Salida de docker network ls mostrando la red java-net
![Red creada](capturas/02-red-creada.png)
## 3. Salida de docker volume inspect mysql-data
![Volumen MySQL](capturas/03-volumen-creado.png)
## 4. Salida de docker ps con ambos contenedores activos
![Contenedores activos](capturas/04-contenedores-corriendo.png)
## 5. docker network inspect java-net con ambos contenedores en la red
![Inspección de red](capturas/05-network-inspect.png)

## **Parte 2 — MySQL (3 capturas)**
## 6. Logs de MySQL mostrando: ready for connections
![Logs de MySQL](capturas/06-mysql-logs.png)
## 7. Salida de SHOW DATABASES; mostrando la base appdb
![Bases de datos](capturas/07-mysql-databases.png)
## 8. Salida de SELECT * FROM usuarios; con los datos del init.sql
![Datos de usuarios](08-mysql-tabla.png)

## **Parte 3 — Payara Admin Console / GUI (5 capturas)**
## 9. Pantalla de login de Admin Console en http://localhost:4848
![Login de Admin Console](capturas/09-payara-login.png)
## 10. Dashboard principal de Payara tras iniciar sesión
![Dashboard de Payara](capturas/10-payara-dashboard.png)
## 11. Pantalla del Connection Pool MySQLPool creado
![Connection Pool MySQLPool](capturas/11-connection-pool.png)
## 12. Resultado del botón Ping mostrando conexión exitosa a MySQL
![Ping a MySQL](capturas/12-ping-exitoso.png)
## 13. JDBC Resource jdbc/MySQLDS visible en la consola
![JDBC Resource](capturas/13-jdbc-resource.png)

## Parte 4 — Conectividad entre contenedores (1 captura)
## 14. Salida del ping de Payara hacia mysql-container desde la terminal
![Ping de Payara a MySQL](capturas/14-ping-contenedores.png)


