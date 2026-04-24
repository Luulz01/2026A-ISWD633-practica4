# Limitar uso de procesador
Limitar la cantidad de núcleos de CPU:
```
--cpus=<número de núcleos>
```

Asignar núcleos de CPU específicos:
```
--cpuset-cpus=<lista de núcleos>
```

**¿Como saber el numero de procesadores virtuales que tiene una máquina?**
## COMPLETAR

**En una máquina virtual (Linux)**

Comando nproc

Comando lscpu

**En una máquina virtual (Windows)**

echo %NUMBER_OF_PROCESSORS%

## Ejemplos
_Puedes copiar y ejecutar directamente cada uno de los comandos_

Limitar el uso de CPU a 1.5 núcleos
```
docker run -d --name server-nginx --cpus="1.5" nginx:alpine
```

<img width="733" height="64" alt="{5638B9AC-159B-4F13-8BA6-784A88186DAA}" src="https://github.com/user-attachments/assets/b0c071bc-8b5e-4108-931a-f7eaec010401" />


Restringir el contenedor para que use los núcleos de CPU 0 a 2:
```
docker run -d --name server-nginx --cpuset-cpus="0-2" nginx:alpine
```
<img width="779" height="69" alt="{CCF8E0BB-AC1F-45C8-BA55-5823D0128E48}" src="https://github.com/user-attachments/assets/5afa0529-34a4-43ee-9c5c-de0800e86ebf" />


Restringir el contenedor para que use los núcleos de CPU 1 y 3:
```
docker run -d --name server-nginx --cpuset-cpus="1,3" nginx:alpine
```
<img width="797" height="69" alt="{0C023D21-FB4E-428D-B03A-690F796B1F13}" src="https://github.com/user-attachments/assets/e57c6bdd-f222-41ee-819d-5ec3566591ec" />

