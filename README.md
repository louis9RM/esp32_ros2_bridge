# esp32_ros2_bridge
Proyecto de comunicación inalámbrica entre un ESP32 con micro-ROS y un entorno ROS 2. El objetivo es controlar la velocidad y posición de actuadores, algunos equipados con encoders, mediante tópicos ROS 2 y un agente micro-ROS ejecutado en Docker. Incluye publicación de datos de sensores y suscripción a comandos de control.

# 🚀 1. Preparación del entorno en la PC (Windows)

### 1.1 Verificar Docker
```bash
docker --version
```

---

### 1.2 Descargar la imagen base de ROS 2 Humble
```bash
docker pull ros:humble-ros-base
```

---

# 🚀 2. Crear el contenedor ROS 2
---
Crear y ejecutar un contenedor Docker con la imagen ros:humble-ros-base:

```bash
docker run -it --name ros2_dev --net=host ros:humble-ros-base bash
```
Verificar variables ROS:
```bash
printenv | grep ROS
```
NOTA: si reinicias la PC y deseas entrar  al contenedor  usar estos paso :

Listar los contenedores existentes:
```bash
docker ps -a
```

Iniciar tu contenedor (si está apagado):
```bash
docker start ros2_dev
```

Entrar a la terminal del contenedor:
```bash
docker exec -it ros2_dev bash
```

# 🚀 3. Preparar el contenedor para instalar micro-ROS Agent

Ejecutar el siguiente comando dentro del contenedor ROS 2:

```bash
apt update && apt install -y git build-essential python3-pip
```
Instalar colcon dentro del contenedor:
```bash
pip3 install -U colcon-common-extensions
```
# 🚀 4. Instalar micro-ROS Agent

Ejecuta dentro del contenedor:
```bash
mkdir -p microros_ws/src
cd microros_ws/src
git clone -b humble https://github.com/micro-ROS/micro-ROS-Agent.git
```
Clonar micro_ros_msgs en el mismo workspace:
```bash
cd ~/microros_ws/src
git clone -b humble https://github.com/micro-ROS/micro_ros_msgs.git
```
Para micro-ROS por WiFi (UDP):
```bash
ros2 run micro_ros_agent micro_ros_agent udp4 --port 8888
```
# 🚀 5. Instalar ESP-IDF en Windows
Ve a la página oficial:
```bash
https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html
```
Descarga el instalador:

ESP-IDF Tools Installer

Instala ESP-IDF para ESP32 (versión recomendada: v4.4 o v5.x)

Abre la consola:

ESP-IDF PowerShell o ESP-IDF Command Prompt

Una vez dentro del terminal de ESP-IDF, ejecutas:
```bash
idf.py create-project microros_esp32
```
Luego clonas el repositorio de micro-ROS para ESP-IDF:
```bash
git clone https://github.com/micro-ROS/micro_ros_espidf_component.git components/micro_ros_espidf_component -b humble
```


