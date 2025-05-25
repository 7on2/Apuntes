## Actualizar paquetes del sistema

```bash
sudo apt update
sudo apt upgrade -y
```
## Eliminar versiones anteriores de Docker (si existen)

```bash
sudo apt remove --purge docker docker.io containerd runc
sudo apt autoremove -y
```
## Instalar dependencias necesarias

```bash
sudo apt install -y ca-certificates curl gnupg
```
## Agregar la clave GPG de Docker

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
## Agregar el repositorio de Docker

```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
## Actualizar los índices de paquetes e instalar Docker

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
==Con las últimas versiones de Docker, Docker Compose está incluido como un plugin, por lo que ya no es necesario instalarlo por separado==
## Verificar que Docker está instalado

```bash
docker --version
```

# Eliminar contenedores 

## Un solo comando 

```bash
docker system prune -a --volumes
```

Esto elimina:

- Todos los contenedores detenidos
- Todas las redes no utilizadas
- Todas las imágenes no referenciadas
- Todos los volúmenes no utilizados
> Este comando borra TODO lo que no esté en uso, incluyendo datos persistentes (¡ten cuidado!).

## Paso a Paso

### Contenedores

- **Eliminar todos los contenedores detenidos:**

```bash
docker container prune
```

- **Eliminar un contenedor específico:**
 
```bash
docker rm <container_id>
```
### Imágenes

- **Eliminar todas las imágenes sin usar:**

```bash
docker image prune -a
```

- **Eliminar una imagen específica:**

```bash
docker rmi <image_id>
```

### Volúmenes

- **Eliminar todos los volúmenes no usados:**

```bash
docker volume prune
```

- **Eliminar un volumen específico:**

```bash
docker volume rm <volume_name>
```

### Redes

- **Eliminar todas las redes no usadas:**

```bash
docker network prune
```

- **Eliminar una red específica:**
 
```bash
docker network rm <network_name>
```

### Tips adicionales

- Para **ver contenedores detenidos**:

```bash
docker ps -a
```

- Para **ver volúmenes**:

```bash
docker volume ls
```

- Para **ver redes**:

```bash
docker network ls
```

# Instalacion de Portainer
## Crear un volumen para los datos de Portainer

```bash
docker volume create portainer_data
```

## Iniciar el contenedor de Portainer

```bash
docker run -d \
  -p 8000:8000 \
  -p 9443:9443 \
  --name=portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest
```
## Verificar que Portainer está corriendo

```bash
docker ps
```
## Probar Docker

```bash
docker run hello-world
```