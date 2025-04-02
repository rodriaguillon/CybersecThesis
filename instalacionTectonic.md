# Guía de Instalación y Uso de Tectonic (Cyber Range GSI-FING)

Esta guía detalla paso a paso cómo instalar y desplegar escenarios de ciberseguridad usando **Tectonic**, desarrollado por el GSI de FING (Udelar). Ideal para preparación de laboratorios, enseñanza o pruebas de tesis.

---

## 📦 1. Instalación de Dependencias en Ubuntu

### 🔧 Actualizar el sistema

```bash
sudo apt-get update
```

### 🧰 Instalar paquetes base necesarios

```bash
sudo apt-get install -y python3 python3-pip build-essential pkg-config libvirt-dev python3-dev
```

---

## 🌍 2. Instalar Terraform y Packer

### Agregar repositorio de HashiCorp

```bash
sudo apt-get install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main" |   sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt-get update
```

### Instalar herramientas

```bash
sudo apt-get install terraform
sudo apt install packer ansible -y
```

Verificar versiones:

```bash
terraform -v
packer -v
ansible --version
```

---

## 🧠 3. Clonar el repositorio de Tectonic

```bash
git clone https://github.com/GSI-Fing-Udelar/tectonic.git
cd tectonic/
```

---

## ⚙️ 4. Instalar Tectonic CLI (python)

```bash
python3 -m pip install --user tectonic-cyberrange
```

Agregar al PATH en `.bashrc` o `.zshrc`:

```bash
export PATH=$HOME/.local/bin:$PATH
source ~/.bashrc  # o source ~/.zshrc
```

Verificar:

```bash
tectonic --help
```

---

## 🐳 5. Configurar Docker (si se usa `platform = docker`)

### Verificar si Docker está instalado:

```bash
docker version
```

### Si no funciona, iniciar Docker Desktop:

```bash
systemctl --user start docker-desktop
docker info
```

> Si falla, asegurate de estar usando **Docker Desktop** y no `docker.io` clásico que puede dar conflictos con `containerd`.

---

## 🧪 6. Probar escenario de ejemplo

Editar archivo `tectonic.ini` y asegurarse de tener:

```ini
[config]
platform = docker
lab_repo_uri = ./examples
```

### Desactivar elastic temporalmente para evitar errores:

Editar `examples/password_cracking.yml`:

```yaml
elastic_settings:
  enable: no
```

### Ejecutar escenario:

```bash
tectonic -c tectonic.ini examples/password_cracking.yml deploy --images
```

> El primer run crea imágenes base con Packer y luego instancia las máquinas virtuales (o contenedores).

---

## ✅ 7. Verificar funcionamiento

- Para Docker:
```bash
docker ps
```

- Para ver logs:
```bash
tectonic --debug ...
```

---

## 🧼 8. Limpiar escenarios

Para destruir instancias:

```bash
tectonic -c tectonic.ini examples/password_cracking.yml destroy
```

---

## 📎 Notas

- Si falla por "imagen 'elastic' no encontrada", desactivar Elastic en el YAML como se indica arriba.
- Si falla `docker.sock`, asegurate de que el daemon esté activo (`docker info` debería responder).

---

## 🎯 Listo

Con esto tenés Tectonic instalado, funcional y con tu primer escenario desplegado. Ideal para entrenar Red Team, Blue Team y prácticas forenses. 🧠💻
