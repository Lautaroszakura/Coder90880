EJERCICIO: Laboratorio Seguro
Alumno: Szakura Lautaro Iván
Comision: 90880
1.	Introduccion
El establecimiento de un entorno de prueba virtualizado es una práctica fundamental dentro del ámbito de la ciberseguridad y la administración de sistemas.
La virtualización permite ejecutar múltiples sistemas operativos “Simulados” de forma simultánea sobre una misma computadora física “Host”, creando un entorno aislado (una especie de bunker) para probar herramientas, configuraciones y software potencialmente peligroso sin poner en riesgo la computadora principal
Los elementos que componen este ecosistema son:
-	Host, es el equipo físico, se compone del hardware real, es el territorio que se buscara proteger
-	Guest, es la máquina virtual, es un sistema operativo simulado (Windows/Linux) que existe como un conjunto de archivos dentro del Host
-	Hipervisor, es el software, en nuestro caso VirtualBox, es el software que administrara y prestara recursos del Host al Guest de forma controlada

2.	Vectores de riesgo y ruptura de aislamiento
Una máquina virtual no es 100% invulnerable por defecto, El malware o un atacante pueden escapar del entorno virtualizado si se activan puentes no seguros entre Host y el Guest, como pueden ser:
-	Carpetas compartidas, Permitir el acceso de la VM a carpetas del Host facilita que un Ransomware o Malware infecte archivos reales
-	Portapapeles compartidos, Copiar y pegar datos entre ambos sistemas puede ser un vector de filtración o transmisión de código malicioso
-	Configuración de red inadecuada, si la VM está conectada a la red local puede escanear o atacar otros dispositivos físicos

3.	Modos de red en VirtualBox
La elección del modo de red determina el nivel de contención del laboratorio según el análisis o prueba a realizar
•	Red interna, Es un bunker total, se utiliza para análisis de malware y ataques controlados entre VMS
•	Solo-Anfitrión: hay una transferencia segura de archivos Host-Guest, sin salida a internet
•	NAT: Hay una descarga segura de herramientas o actualizaciones del sistema
•	Puente, Expone a la VM a la red física domestica o empresarial
•	
Modo de red	Acceso a internet	Conexión con Host	Conexión a red Local
Red interna	No	No	No
Host-Only	No	Si	No
NAT	Si	No	No
 Puente	Si	Si	Si

4.	Instructivo de instalación de Entorno seguro
a)	Una vez descargado VM, y también descargada la ISO, del sistema operativo que se desee virtualizar (Para este trabajo se usó una imagen ISO de Kali Linux) 
Se montará la imagen ISO en la VM y se ira configurando

<img width="436" height="384" alt="image" src="https://github.com/user-attachments/assets/079db45c-0280-484a-b1e8-131e06ce3688" />

b)	Se le asignara cantidad de memoria RAM y Cantidad de CPU

<img width="458" height="410" alt="image" src="https://github.com/user-attachments/assets/a849e0f4-b511-4df4-9211-f8f1e91a3bff" />

c)	En este paso se le asignara el tamaño total que tendrá el disco de la maquina virtual, el cual luego, en el proceso de instalación se particionara, según los requerimientos

<img width="431" height="379" alt="image" src="https://github.com/user-attachments/assets/eff27416-592f-4bb6-8d45-0e33612bffca" />

d)	Una vez seleccionadas las configuraciones de la VM, se abrirá el panel de redes, y se seleccionara la opción “Internal Network”, la cual nos permitirá un aislamiento total de la Maquina virtual a la Maquina Host, además que se podrá proteger la red local, y la comunicación Host-Guest será de manera controlada

<img width="448" height="217" alt="image" src="https://github.com/user-attachments/assets/eaaefbf0-b27c-4f81-9949-6fa3deed2293" />

e)	Previo al proceso de instalación, se observa que todos los datos cumplan con los requerimientos

<img width="334" height="334" alt="image" src="https://github.com/user-attachments/assets/63461931-1ea4-4bad-b374-23dfb8bebc8b" />

f)	Como consecuencia del modo de red elegido, al momento de la instalación, se alertará al usuario que la maquina no esta conectada a ninguna red, ni posee IP alguna\

<img width="365" height="313" alt="image" src="https://github.com/user-attachments/assets/da509f18-c80d-4195-835f-7e2defe61cc1" />

g)	Una vez finalizada la instalación, y como paso final antes de comenzar a utilizarla, se tomará una Snapshot, la cual es un punto de restauración, en caso de que la maquina se rompa, o se ejecute algún malware

<img width="461" height="469" alt="image" src="https://github.com/user-attachments/assets/292db03c-64f7-40ee-9c1a-b995aaa20ece" />

