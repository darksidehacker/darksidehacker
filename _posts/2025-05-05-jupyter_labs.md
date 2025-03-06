---
layout: post
title: Setting Up Jupyter Notebooks & Labs
date: 2025-03-05 15:09:00
description: Configure Jupyter Lab for Jetson Platform
tags: Jetson Software
categories: Work
featured: false
---

JupyterLab es un entorno de trabajo interactivo que se ejecuta en tu navegador web. Permite escribir y ejecutar código en varios lenguajes de programación, así como visualizar datos y crear documentos interactivos llamados "cuadernos".

Creado por el Proyecto Jupyter, JupyterLab sirve para explorar y analizar datos, desarrollar modelos de aprendizaje automático, realizar cálculos científicos y crear informes interactivos. Es una herramienta popular entre científicos de datos, programadores e investigadores debido a su flexibilidad y facilidad de uso. Ademas es muy conveniente instalarlo en la Jetson Nano.

1. Actualizar el sistema

````markdown
```c++
code code code
```
````

```c++
sudo apt update
sudo apt upgrade -y
```

Instalar JupyterLab usando pip:

```c++
pip3 install jupyterlab
```

Configurar JupyterLab en una red ya que por defecto, JupyterLab solo es accesible desde la máquina local.

- 1. Generar un archivo de configuración:

```c++
jupyter-lab --generate-config
```

- 2. Crear una contraseña para JupyterLab:
     Ejecuta el siguiente comando y sigue las instrucciones para crear una contraseña:

```c++
jupyter-lab password
```

- 3. Editar el archivo de configuración:
     Abre el archivo de configuración generado:

```c++
nano ~/.jupyter/jupyter_server_config.py
```

- 4. Modificar, crear o simplemente descomentar estas lineas utilizando vim o nano

```c++
c.ServerApp.ip = '0.0.0.0'  # Permite acceso desde cualquier IP
c.ServerApp.open_browser = False  # No abrir el navegador automáticamente
c.ServerApp.port = 8888  # Puerto por defecto (puedes cambiarlo si es necesario)
```

Para iniciar JupyterLab, ejecuta:

```
jupyter-lab
```

---

## (Opcional) Ejecutar JupyterLab como un servicio

Si deseas que JupyterLab se inicie automáticamente al encender la Jetson Nano, puedes configurarlo como un servicio.

Crear un archivo de servicio:

```
sudo nano /etc/systemd/system/jupyterlab.service
```

Agregar el siguiente contenido:

```
[Unit]
Description=JupyterLab
After=network.target

[Service]
User=<tu-usuario>  # Reemplaza con tu nombre de usuario
WorkingDirectory=/home/<tu-usuario>  # Reemplaza con tu directorio de inicio
ExecStart=/usr/local/bin/jupyter-lab --config=/home/<tu-usuario>/.jupyter/jupyter_server_config.py
Restart=always

[Install]
WantedBy=multi-user.target
```

Habilitar y iniciar el servicio:

```
sudo systemctl daemon-reload
sudo systemctl enable jupyterlab
sudo systemctl start jupyterlab
```

Verifica que el servicio esté activo:

```
sudo systemctl status jupyterlab
```
