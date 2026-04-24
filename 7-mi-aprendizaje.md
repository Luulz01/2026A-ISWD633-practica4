# MI APRENDIZAJE


### Problema
**1) Ejecutar el archivo Dockerfile y construir una imagen en la versión 1.0**
   
Durante el proceso de construcción de la imagen se presentó un error al ejecutar el comando yum update, debido a que los repositorios oficiales de CentOS 7 ya no se encuentran activos.

<img width="1296" height="978" alt="{7EA39EC5-E23C-4260-9A4C-AA92392DD289}" src="https://github.com/user-attachments/assets/84c45f3a-2e85-46f9-b9a4-59184fd18db0" />

Según lo que investigué esto ocurre porque CentOS 7 ha llegado a su fase de fin de vida (EOL - End Of Life), lo que significa que:

Sus repositorios principales han sido deshabilitados
Ya no reciben actualizaciones oficiales
Las URL originales (mirrorlist) dejan de funcionar

Para solucionar este problema, se modificó la configuración de los repositorios dentro del contenedor con el siguiente comando:

RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-Base.repo && \
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-Base.repo

El repositorio vault contiene versiones archivadas de CentOS que aún pueden ser utilizadas para instalación de paquetes. Con dicho cambio se logró ejecutar adecuadamente la creación de la nueva imagen.

<img width="1280" height="511" alt="{8B35F532-F205-4979-85E7-FFA09A7D710C}" src="https://github.com/user-attachments/assets/a7e570ba-07ee-4c03-be15-83eff3874a4f" />
