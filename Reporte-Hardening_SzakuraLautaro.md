Mi Primer Laboratorio seguro de Ciberseguridad

Alumno: Szakura Lautaro Iván

Comisión: 90880

1.	La fundación: VirtualBox y Red aislada
Para el desarrollo de las practicas del laboratorio se selecciono Kali Linux como sistema operativo principal. Esta es una distribución, basada en Debian, y está diseñada específicamente para auditorias de seguridad, pruebas de penetración y análisis forenses.
También incluye herramientas de seguridad como (Nmap, Wireshark, Metasploit, entre otras), las cuales serán de utilidad a lo largo del curso
La interfaz de red de la VM fue configurada en modo NAT, la elección responde a criterios de aislamiento, control de tráfico y protección del Host
-	En modo NAT, el hipervisor actúa como un router/firewall virtual entre sistema operativo Host y la VM.
Se impedirá que la máquina virtual sea visible como un modo de red activo para otros dispositivos conectados al Wi-Fi o red física loca
-	Se tendrá un acceso a internet unidireccional controlado, permite que Kali inicie conexiones salientes hacia internet utilizando la dirección IP publica/local. Y Se bloquea por defecto cualquier intento de conexión entrante no solicitada desde la red local o externa hacia la VM
-	Al tratarse de una distribución con herramientas ofensivas y servicios, el modo NAT garantiza que el trafico generado en las pruebas no se filtre hacia la red domestica
A diferencia del modo Bridge, el cual expondría a la VM directamente en la red física, el modo NAT encapsula el entorno de pruebas, protegiendo el equipo real y a otros dispositivos

<img width="255" height="317" alt="image" src="https://github.com/user-attachments/assets/b6feb025-9b62-48e8-817d-ee72ce84c2b5" />

2.	Capa de sistema operativo: Usuarios y Parches
Para cumplir con las buenas practicas de seguridad informática, la administración del sistema se separó del uso cotidiano
El sistema operativo Linux separa estos dos, mediante:
-	Cuenta de usuario estándar, la cual es utilizada para las actividades prácticas y la navegación diaria sin privilegios elevados
-	Usuario Root, utilizada principalmente para tareas de mantenimiento, instalación de Software y configuración de sistema 

<img width="717" height="372" alt="image" src="https://github.com/user-attachments/assets/8578a077-10d9-43d9-abf4-b7fa0946919e" />

Para esta imagen se utilizo otra VM instalada sobre Debian, pero se puede apreciar la diferencia entre un usuario estándar (laucha@Debian) y un usuario root (root@Debian), cabe destacar que mediante el mismo prompt “rmdir /etc” el primero al no tener los permisos necesarios no podrá borrar el directorio /etc el cual es de importancia para la VM, mientras que el usuario root lo podrá borrar sin ninguna advertencia sobre su importancia

3.	Capa Linux: Permisos y gestión del sistema
Para este apartado, se crearán dos archivos, uno mediante un usuario estándar, y otro mediante un usuario root y se verán sus permisos mediante el comando “ls -l”

<img width="886" height="462" alt="image" src="https://github.com/user-attachments/assets/f5f75f09-99a2-4681-9f51-e3684c5a1363" />
 
Se crearon los archivos archivo1.txt y archivo2.txt cada un con un usuario distinto, dado que solo son archivos de texto, se le otorgaron los mismos permisos (r-lectura, w-escritura), pero en la segunda y tercera columna se puede ver el usuario y el grupo propietario respectivamente

Consulta de repositorios y paquetes

Para verificar el estado de los paquetes de software y garantizar la integridad de las fuentes de instalación, se usará el comando “apt Update” el cual como se muestra a continuación se tiene que realizar mediante la cuenta root dado que se descargaran y sobreescribiran archivos para los cuales se necesitan permisos especiales de root.

<img width="886" height="466" alt="image" src="https://github.com/user-attachments/assets/509e99bc-1f95-43b1-8370-bd2fdbde2a00" />
<img width="886" height="462" alt="image" src="https://github.com/user-attachments/assets/56e77043-9c76-456d-9e6d-4a18b2b82663" />

4.	La red de seguridad: Snapshot inicial
Antes de finalizar la fase de preparación se aplico un Hardening básico
-	Sistema totalmente actualizado
-	Usuario estándar configurado (usuario diario/root)
-	Servicios innecesarios desactivados (Aplica para sistema Windows)
Para lo cual se creo un punto de restauración estático en VirtualBox denominado: “Clean Install – Hardening applied”

<img width="885" height="392" alt="image" src="https://github.com/user-attachments/assets/19254ea7-3303-4748-b46c-72adf8b46e38" />

Cuyo propósito funciona como un punto de retorno seguro, en caso de que futuras pruebas desconfiguren el sistema, infecten la maquina con malware de prueba o provoquen inestabilidad, es posible revertir la VM a este estado limpio en segundos sin requerir una reinstalacion

5.	Conclusión

El despliegue de la Maquina de practicas se completo exitosamente estableciendo una base técnica solida y alineada con estándares básicos de Ciberseguridad
La implementación del modo NAT, garantiza un entorno de red aislado que permite el trafico saliente controlado sin exponer la maquina anfitriona ni la red local a posibles amenazas
La configuración de Kali Linux aplicando la segregación de cuentas (usuario estándar/root) refuerza el principio de menor privilegio, asegurando que las herramientas operen bajo un esquema de acceso controlado
También la aplicación de parches de seguridad y la creación del Snapshot inicial dotan al laboratorio de resiliencia operativa. Esta “Maquina del tiempo” asegura la capacidad de revertir cualquier fallo, infección o desconfiguración derivada de futuras pruebas en cuestión de segundos, dejando el entorno listo y protegido para la ejecución segura de auditorias y pruebas de penetracion.
