# Proyecto-final-infraestructura

Se agregan los 9 discos que piden para los RAIDS, esto debe hacerse afuera con la máquina apagada para evitar inconvenientes
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/agregarDiscos.png?raw=true)

Ahora se “activan” los discos agregados anteriormente. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/activacionDiscos.png?raw=true)

Listamos los discos con el comando sudo fdisk -l 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/discosListados1.png?raw=true)

![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/discosListados2.png?raw=true)

![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/discosListados3.png?raw=true)

Se crean los 3 RAIDS con 3 discos agregados para cada RAID. 

RAID1: sdb, sdc, sdd 

RAID2: sde, sdf, sdg 

RAID3: sdh, sdi, sdj  
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/creacionRAIDS.png?raw=true)

Listamos los archivos especiales que representan los dispositivos de hardware y otros recursos del sistema. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/listadoArchivosEspeciales.png?raw=true)

Mostrando el estado de los RAIDS, permitiendo monitorear si están activos, el nivel y estado de los discos que la componen.
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/estadoMatricesRAIDS.png?raw=true)

Inicializar los RAIDS como volúmenes físicos.
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/iniciarRAIDSVolumenesFisicos.png?raw=true)

Ahora se listan todas las unidades físicas que forman parte de algún grupo de volúmenes. Se muestran como los tres discos (RAIDS) se ven configurados como volúmenes físicos dentro de lvm2, cada uno con 2 GB y con espacio disponible. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/listadoUnidadesFisicasGrupoVolumenes.png?raw=true)

A continuación, se crea un nuevo grupo de Volumen llamado vgproyecto, agrupando los volúmenes físicos mostrados en el paso anterior. Esto permite administrar estos discos como una sola unidad lógica. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/creacionGrupoVolumenVgproyecto.png?raw=true)

Ahora se listan todos los grupos de volúmenes. Muestra la información del grupo de volumen creado, incluyendo su tamaño total, espacio libre, número de volúmenes físicos, etc. En este caso, se confirma que vgproyecto tiene 5.99 GB disponibles. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/listadoGruposVolumenes.png?raw=true)

Creamos un volumen lógico con nombre lvmapache, lvmmysql, lvmnginx dentro del grupo de volúmenes lógicos vgproyecto. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/creacionVolumenLogico.png?raw=true)

Se muestran los volúmenes lógicos creados dentro del grupo vgproyecto, incluyendo sus nombres y tamaños. En este caso se visualizan tres volúmenes lógicos de 1 GB cada uno. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/volumenesLogicosVgproyecto.png?raw=true)

Se crean los repositorios apache, mysql y nginx, posteriormente los listamos.
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/creacionRepositoriosListados.png?raw=true)

Se utiliza mkfs.ext4 para formatear cada volumen lógico (lvmapache, lvmmysql y lvmnginx) con el sistema de archivos EXT4. Esto lo que hace es que deja listo para que cada volumen pueda ser montado y usado por el sistema. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/formateoVolumenLogico.png?raw=true)

Se solicita toda la información relacionada con los volúmenes lógicos que se formatearon anteriormente. Lo subrayado son los volúmenes lógicos y ya se pueden ver montados en el sistema correctamente. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/solicitudInformacionVolumenLogicos.png?raw=true)

Se ejecuta el docker para montar un contenedor de Apache en segundo plano. El contenedor vincula el puerto 8080 del host al puerto 80 del contenedor y monta un volumen local. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/ejecucionDockerContenedorApache.png?raw=true)

Se utiliza el editor de texto nano para crear un archivo index.html. Este archivo será utilizado por el contenedor de Apache desde el volumen montado previamente.
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/editorNanoContenedorApache.png?raw=true)

Se construye una imagen Docker personalizada a partir de un Dockerfile. El proceso muestra los pasos de construcción incluyendo de la imagen base, la copia de archivos, etc. Al finalizar se crea exitosamente una imagen docker llamada “miapache” que será utilizado. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/construccionImagenDockerDockfile.png?raw=true)

A continuación, se monta un contenedor usando la imagen personalizada “miapache” creada anteriormente. El contenedor vincula el puerto 8081 del host al puerto 80 del contenedor y sube el mismo volumen local de Apache. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/contenedorPuerto8081.png?raw=true)

Se montaron tres directorios locales en puntos cruciales del sistema. Se vincularon los volúmenes lógicos LVM con directorios específicos para que puedan ser utilizados por los servicios de Apache, MySQL y Nginx respectivamente. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/vinculacionLVMDirectorios.png?raw=true)

Se está editando un archivo de configuración con nano que contiene lo del SQL. Las instrucciones incluyen información para crear una base de datos, para otorgar permisos de acceso, etc. Este archivo será ejecutado para configurar la base de datos. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/edicionNanoSQL.png?raw=true)

Se está editando un Dockerfile con nano para construir una imagen personalizada de MySQL. Especifica la imagen base y utiliza el comando copy para copiar todo el archivo desde el host a el contenedor. Permite las conexiones a la base de datos. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/nanoDockerfileMySQL.png?raw=true)

Se construye una imagen Docker personalizada de MySQL a partir de Dockfile. Esto muestra los diferentes pasos junto con la descarga y las diferentes instalaciones. Al finalizar, se genera una imagen llamada “mimysql” lista para ser utilizada en los contenedores. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/construccionImagenDockerMySQL.png?raw=true)

Se listan todos los contenedores Docker activos en el sistema. La salida muestra los contenedores en ejecución, las imágenes utilizadas, el tiempo de creación, etc. También se observa el arranque del contenedor MySQL con configuraciones específicas.

![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/servidorMySQL.png?raw=true)

Se conecta al servidor MySQL que corre en el contenedor Docker. Se ejecutan varias peticiones SQL, para seleccionar la base de datos, creación de una tabla “prueba” con id y nombre. El resultado muestra el registro creado.
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/servidorMySQL.png?raw=true)

Se está editando un Dockerfile con nano para construir una imagen personalizada de Nginx. Especifica una imagen base y se copia toda la configuración desde el directorio del host hacia el contenedor.  
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/edicionNanoNginx.png?raw=true)

Se construye una imagen Docker personalizada de Nginx a partir de Dockerfile. El proceso muestra todos los pasos y las descargas necesarias de la imagen base nginx. Al completarse, se genera una imagen llamada “minginx” lista para utilizar. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/construccionImagenNginx.png?raw=true)

A continuación, se ejecuta el contenedor de Nginx usando la imagen personalizada “minginx”. El contenedor se nombra “nginx_container”, vincula el puerto 8082 del host al puerto 80 del contenedor y sube el volumen local hacia la web de Nginx. 
Se listan todos los contenedores Docker activos en el sistema. Muestra los 3 contenedores creados anteriormente (MySQL, Apache y Nginx). Cada uno con su puerto respectivo y con su funcionamiento correcto. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/ejecucionContenedorNginx.png?raw=true)

Finalmente, se accede desde el navegador web a las páginas de los contenedores Docker para verificar su correcto funcionamiento. Se visualizan las páginas en los puertos configurados previamente. Cada contenedor está funcionando correctamente. 
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/ResultadoNginx.png?raw=true)
![alt text](https://github.com/michael-hap/Proyecto-final-infraestructura/blob/main/Imagenes/ResultadoApache.png?raw=true)
 
