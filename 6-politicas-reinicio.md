# Políticas de reinicio

## Para esta parte de la práctica
1. Usa el archivo Dockerfile que se encuentra en cada carpeta con el nombre de la política de reinicio para crear una imagen. Analiza las instrucciones de cada Dockerfile 
2. Usa la imagen para ejecutar un contenedor agregando la política respectiva y observar lo que sucede verificando el cumplimiento de la política de reinicio

### no
No reinicia el contenedor bajo ninguna razón. Esta es la política por default
```
docker run -d --name <nombre contenedor> <nombre imagen>
```

<img width="1095" height="427" alt="{103F5F7D-E54F-4528-BE03-812FEF4695FC}" src="https://github.com/user-attachments/assets/e169ee6e-6f04-4c52-9cd3-67898e3ca220" />


**Politica de reinicio - no**
<img width="615" height="73" alt="{FE4924A0-78C1-404B-9395-234F827FC3C6}" src="https://github.com/user-attachments/assets/a30921e7-85b9-455c-8d53-5185ddcb23fb" />

<img width="1099" height="224" alt="{10EF20B1-C17F-4A55-ADA1-68B52808261C}" src="https://github.com/user-attachments/assets/cde76f85-d81f-46d2-9554-38b3d3fbe01d" />


Al utilizar la política de reinicio por defecto (no), el contenedor se detuvo completamente al ejecutar el comando docker stop y no volvió a iniciarse automáticamente.

### always
Reinicia siempre el contenedor si se detiene. Si se detiene manualmente, sólo se reiniciará cuando se reinicie el demonio Docker o cuando se reinicie manualmente el propio contenedor
```
docker run -d --name <nombre contenedor> --restart always <nombre imagen>
```

<img width="1100" height="471" alt="{0099D36A-4FAB-4A29-817F-A2DFCC54FD38}" src="https://github.com/user-attachments/assets/061fcb86-203e-485d-893d-42dc8e2c3468" />

**Politica de reinicio - always**
<img width="813" height="61" alt="{C667F569-3175-47DC-B844-D6D2C78BF228}" src="https://github.com/user-attachments/assets/091f41aa-abe3-4c36-8680-09a9b83da0c5" />

<img width="1048" height="168" alt="{2B931B11-5A79-47D0-8F5B-1B599E4DE945}" src="https://github.com/user-attachments/assets/eb0d3f2f-39c5-4a70-a9e6-cb1a093b07eb" />


### unless-stopped

Similar a always, excepto que cuando el contenedor se detiene (manualmente o de otra manera), no se reinicia incluso después de reiniciar el demonio Docker.
```
docker run -d --name <nombre contenedor> --restart unless-stopped <nombre imagen>
```


<img width="1088" height="488" alt="{1A4136E5-1DE2-4491-B087-DDD29EBDB203}" src="https://github.com/user-attachments/assets/8faedd58-3b64-4354-9e91-50129c5e7803" />


<img width="998" height="73" alt="{1B9C3693-3A47-4914-AAAF-6242694F3A3D}" src="https://github.com/user-attachments/assets/98b181de-ca58-4bf5-88e8-4701cae810f4" />


<img width="1065" height="471" alt="{A3664891-8FC8-44D6-A68F-F6FD7B7FF9FD}" src="https://github.com/user-attachments/assets/6195baa8-37b8-438e-9a63-4b53a5ca55ed" />


### on-failure
Se reinicia únicamente cuando hay una falla en la ejecución del código que se manifiesta con un código diferente de 0. No se reinicia si el contenedor se detiene manualmente.

```
docker run -d --name <nombre contenedor> --restart on-failure <nombre imagen>
```
