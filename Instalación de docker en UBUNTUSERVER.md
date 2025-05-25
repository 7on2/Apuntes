# Instalación de docker en UBUNTUSERVER

## Instalación de Docker en Ubuntu Server

Actualice el `apt`índice de paquetes e instale paquetes para permitir `apt`el uso de un repositorio a través de HTTPS:

```bash
sudo apt-get update
sudo apt-get install
ca-certificates curl lgnupg
```

Agregue la clave GPG oficial de Docker:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

Use el siguiente comando para configurar el repositorio:

```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Actualice:

```bash
sudo apt-get update
```

**Instalar el motor Docker**
1.Instale Docker Engine, containerd y Docker Compose.

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verifique que la instalación de Docker Engine se haya realizado correctamente ejecutando la `hello-world`imagen.

```bash
 sudo docker run hello-world
```

Este comando descarga una imagen de prueba y la ejecuta en un contenedor. Cuando se ejecuta el contenedor, imprime un mensaje de confirmación y sale.

**¿Cómo es el proceso de creación de imágenes y contenedores?**

Cuando ejecutas el comando **`sudo docker run hello-world`**, no estás creando una nueva imagen, sino que estás ejecutando un contenedor basado en la imagen "hello-world" que ya existe.

Aquí te explico lo que sucede paso a paso:

1. Docker busca la imagen llamada "hello-world" en tu sistema local. Si no la encuentra, descargará automáticamente la imagen desde Docker Hub, que es un registro público de imágenes de Docker.
2. Una vez que Docker tiene la imagen "hello-world", crea un nuevo contenedor basado en esa imagen.
3. El contenedor recién creado se inicia y ejecuta un programa muy simple que imprime un mensaje de "Hello, World!" en la salida estándar.
4. Después de imprimir el mensaje, el contenedor se detiene automáticamente porque no hay ningún proceso en ejecución dentro del contenedor una vez que se ha completado el mensaje.

Así que, en resumen, no estás creando una nueva imagen al ejecutar `sudo docker run hello-world`. Simplemente, estás utilizando la imagen existente para crear y ejecutar un contenedor temporal con un programa sencillo que imprime "Hello, World!"
