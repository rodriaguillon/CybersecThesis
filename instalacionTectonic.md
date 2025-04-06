# Tectonic Lab - Setup Básico

Este README documenta el proceso de instalación de Tectonic hasta la parte de configuración *previa a AWS*, más algunos ajustes personalizados necesarios para levantar escenarios localmente sin Elastic.

---

### Seguir los pasos de este link 

- https://github.com/GSI-Fing-Udelar/tectonic/blob/main/docs/installation.md
- Hasta la sección que habla de AWS.

### Luego setear el ambiente

- Modificar tectonic.ini:
    - lab_repo_uri = /home/rodrigo/tectonic/examples (aca poner donde esta tectonic/examples)
    - ssh_public_key_file = ~/.ssh/raguillon_id_rsa.pub (aca poner la ruta al id de la clave pública)


- Modificar examples/password_cracking/description.yml:

    - elastic_settings:
        - enable: no


### Ejecutar el docker que levante el ambiente

- tectonic -c tectonic.ini examples/password_cracking.yml deploy --images

### Descubrir las IP de acada contenedor (victim y attacker)

- `docker ps`
- `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' e7c231c21b4f` (el último parámetro es el número del contendor)
- A partir de ahi sabemos la IP tanto del attacker tanto como del victim.

- Luego ejecutamos: `docker exec -it monstersinc-passwordcracking2024-1-attacker bash`
- Desde el usuario trainee seguimos toda la documentación que se encuentra en el README de password_cracking.
- Te facilito la lista de usuarios sin email que vas a tener que probar la password con el comando de HYDRA:

## Posibles usuarios sin email público (para fuerza bruta con Hydra)

La siguiente lista fue generada a partir del archivo `employees.html`, incluyendo únicamente aquellos empleados que **no tenían dirección de correo electrónico publicada**. Se supone que los nombres de usuario siguen el patrón: inicial del nombre + apellido (todo en minúsculas y sin tildes).

```txt
halagia
aarevalo
gbandieri
abrunetti
mbuteler
pcalatayud
ccirelli
adiscala
jescobar
rfernández
pferreyra
pgleiser
pgrosman
rguibert
jjuarez
dlescano
amajtey
rmellano
fmiotti
rnieto
moliva
epilotta
oreula
crosas
cschurrer
murciuolo
surreta
nveglio
nwolovick
mzuriaga
``` 