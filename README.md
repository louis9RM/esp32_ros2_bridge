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
Crear y ejecutar un contenedor Docker con la imagen ros:humble-ros-base:
```bash
docker run -it --name ros2_dev --net=host ros:humble-ros-base bash
```
