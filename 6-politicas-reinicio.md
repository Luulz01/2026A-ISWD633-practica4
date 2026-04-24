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

<img width="1144" height="437" alt="{A3AAED5B-235C-4BCA-9706-0F01C5F1ADA0}" src="https://github.com/user-attachments/assets/db925fbc-131d-483b-83cb-f37a8859da82" />


**Politica de reinicio - always**
<img width="813" height="61" alt="{C667F569-3175-47DC-B844-D6D2C78BF228}" src="https://github.com/user-attachments/assets/091f41aa-abe3-4c36-8680-09a9b83da0c5" />

<img width="1092" height="103" alt="{7311950F-D96A-40E9-BC21-B239F255A4C5}" src="https://github.com/user-attachments/assets/e2594cc0-3071-4f08-a2c5-bb97af5b3487" />

<img width="1138" height="749" alt="{97AC3923-A728-4E60-BEF2-AB495A80083B}" src="https://github.com/user-attachments/assets/923cda29-2061-41e4-9660-d206b5fb8a30" />

Stop

<img width="1049" height="213" alt="{7C590C6E-2E4E-4652-A10B-F749FCBF9C34}" src="https://github.com/user-attachments/assets/7830b29c-fe72-4acd-92f7-54f9d21c1138" />


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

<img width="1108" height="500" alt="{FDB4D099-3274-476C-AF6A-7F8BA824D725}" src="https://github.com/user-attachments/assets/de9a2399-e294-48bb-aa5b-69a07ee6ac31" />

<img width="1063" height="169" alt="{8EDA49A7-43B6-4E7C-BD38-42E87CCD6AC4}" src="https://github.com/user-attachments/assets/1042ff35-21b8-408d-bb6e-744bebad5598" />

<img width="1145" height="625" alt="{31D178E8-5969-4050-B391-2178D3BCA3FE}" src="https://github.com/user-attachments/assets/a6d324bb-662e-4981-a7dc-836fdc01d812" />

Se verificó la política on-failure utilizando un script que finaliza con código de error (exit 1). Se observó que el contenedor se reinicia automáticamente, lo cual se evidencia en el valor "RestartCount" que indica múltiples reinicios.
