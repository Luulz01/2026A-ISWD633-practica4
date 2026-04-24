# MI APRENDIZAJE
En esta cuarta práctica trabajé con la creación de imágenes mediante Dockerfile, comprendiendo cómo se construyen paso a paso y cómo cada instrucción genera una capa dentro de la imagen. Además, reforcé el uso de contenedores aplicando configuraciones más avanzadas como políticas de reinicio y limitación de recursos.

También aprendí la importancia del contexto de construcción, verificando que el archivo Dockerfile y los recursos necesarios (como index.html o scripts .sh) estén en el directorio correcto para evitar errores.

### Conocimientos previos
- Uso básico de Docker (docker run, docker ps, docker stop)
- Creación y ejecución de contenedores
- Uso de imágenes desde Docker Hub
- Mapeo de puertos básico

### Conocimientos adquiridos después de la práctica
- Creación de imágenes personalizadas mediante Dockerfile
- Comprensión de instrucciones como FROM, RUN, COPY, EXPOSE y CMD
- Uso del mecanismo de caché de Docker, observando que solo se reconstruyen las capas modificadas
- Identificación y solución de errores comunes (archivos faltantes, nombres incorrectos, rutas)
- Uso de políticas de reinicio (no, always, unless-stopped, on-failure) y su comportamiento real
- Limitación de recursos del contenedor, especialmente el uso de memoria RAM y memoria swap

### Cálculo de memoria swap

Se aplicó la fórmula:

Memoria swap máxima = memory-swap − memory

Ejemplo trabajado:

memory = 300 MB
memory-swap = 1 GB = 1024 MB

Resultado: 724 MB de memoria swap disponible

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

### Cosas que realicé y aprendí
- Construí imágenes desde cero usando Dockerfile
- Modifiqué archivos y observé cómo Docker reutiliza caché
- Ejecuté contenedores con distintas políticas de reinicio y analicé su comportamiento
- Verifiqué cómo Docker reinicia contenedores automáticamente (always)
- Identifiqué cuándo un contenedor falla y entra en bucle de reinicio
- Aprendí a limitar recursos del sistema para evitar consumo excesivo

### Conclusión
Esta práctica me permitió comprender el funcionamiento interno de Docker a un nivel más profundo, especialmente en la construcción de imágenes, optimización mediante caché, control de ejecución automática de contenedores y gestión de recursos. Estos conocimientos son fundamentales para el despliegue eficiente y controlado de aplicaciones en entornos reales.
