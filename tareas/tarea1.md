
# Tarea 1

Esta es una guía para preparar el entorno.


## Instalación de WSL y Ubuntu

Abrir PowerShell como administrador y ejecutar el siguiente comando:

```bash
wsl --install
```

Descargar el instalador de Ubuntu para WSL desde el siguiente enlace: https://ubuntu.com/wsl, y posteriormente ejecutarlo.


## Actualizaciones y zsh

Para actualizar los paquetes del sistema operativo se deben utilizar los siguientes comandos:

```bash
sudo apt update
 
sudo apt upgrade
```

Para instalar la terminal ohmyzsh se debe instalar primero zsh y después ejecutar el siguiente comando:

```bash
sudo apt install zsh

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


## Instalación de Docker

Remover paquetes conflictivos:
```bash
sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-compose-v2 docker-doc docker-buildx podman-docker containerd runc | cut -f1)
```

Añadir los repositorios de Docker con los siguientes comandos:
```bash
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```

Para instalar la ultima versión ejecutar el siguiente comando:
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verificar que el servicio de Docker esté encendido:
```bash
sudo systemctl status docker
```

### Añadir nuestro usuario al grupo docker

La siguiente configuración nos ayudará a agilizar el uso de docker sin tener que utilizar permisos de administrador (sudo).

Crear el grupo docker:
```bash
sudo groupadd docker
```

Añadir usuario al grupo:
```bash
sudo usermod -aG docker $USER
```

Reiniciar la terminal y verificar que se pueda utilizar el comando docker sin sudo.
```bash
docker run hello-world
```


## Instalar python

Instalar paquetes necesarios con los siguientes comandos:
```bash
sudo apt install -y \
make \
build-essential \
libssl-dev \
zlib1g-dev \
libbz2-dev \
libreadline-dev \
libsqlite3-dev \
curl \
llvm \
libncursesw5-dev \
xz-utils \
tk-dev \
libxml2-dev \
libxmlsec1-dev \
libffi-dev \
liblzma-dev
```

Clonar el siguiente proyecto:
```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

Configuraciones necesarias:
```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init - zsh)"' >> ~/.zshrc
source ~/.zshrc
pyenv --version
```

Instalar la versión 3.14.7 de pyenv:
```bash
pyenv install 3.14.7
```

Verificar la versión:
```bash
pyenv versions
```

Establecer la versión en todo el sistema operativo:
```bash
pyenv global 3.14.7
```

Verificar versión de python:
```bash
python --version
```

Crear el directorio para jupyter y entrar:
```bash
mkdir -p ~/jupyter
cd ~/jupyter
```

Crear un entorno virtual para python en el directorio actual (~/jupyter):
```bash
python -m venv .venv
```

Encender el entorno virtual anteriormente creado:
```bash
source .venv/bin/activate
```

Actualizar el gestor de paquetes pip:
```bash
python -m pip install --upgrade pip
```

Instalar los siguiente paquetes para trabajar con Jupyter Notebooks:
```bash
pip install notebook

pip install ipykernel
```

Encender el servidor local de Jupyter:
```bash
jupyter notebook
```
