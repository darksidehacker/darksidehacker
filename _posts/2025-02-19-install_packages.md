---
layout: post
title: Install Packages for Jetson Nano
date: 2025-02-19 15:09:00
description: Install packages for Jetson Nano
tags: Jetson
categories: Work
featured: true
related_posts: false
---

Nuestra meta es instalar la siguiente paqueteria:

        -TensorFlow 1.15.5
        --PyTorch v1.10.0
        --torchvision v0.11.0
        -torchaudio v0.10.0
        --onnx 1.11.0
        --CuPy 9.2.0
        --numpy 1.19.5
        -numba 0.53.1
        -OpenCV 4.5.0 (with CUDA)
        --pandas 1.1.5
        --scipy 1.5.4
        --scikit-learn 0.24.2
        --JupyterLab 2.2.9
        -DarkNet

Opcional:

- ROS
- Darknet
- Deepstream 6.0.1
- OpenCV con soporte CUDA
- Go Lang para ARM
- Julia for ARM

---

Paso 1. Actualizar el sistema

```bash
sudo apt-get update
```

Confirmamos el upgrade

```bash
sudo apt-get -y upgrade && sudo apt-get install python-pip python3-pip
```

Por defecto el soporte para conectar HDD externos no viene instalado por default, la siguiente instrucción lo hara:

```bash
sudo apt install exfat-fuse exfat-utils
```

Finalmente, removeremos LibreOffice y Thunderbird:

```bash
sudo apt remove --purge libreoffice* && sudo apt remove --purge thunderbird*
```

```bash
sudo apt autoremove
```

A continuación instalaremos JTOP, similar a HTOP, una herramienta capaz de monitorizar los recursos de nuestro sistema de forma visual.

```bash
sudo pip3 install -U jetson-stats
```

Y eso es todo, finalmente para probar que se está ejecutando correctamente, lo llamaremos con el siguiente comando. (Después de realizar un reinicio)

```bash
sudo reboot
```

Una vez reiniciado esperamos unos minutos y accedemos de nuevo con SSH y verificamos que Jtop se haya instalado.

```bash
jtop
```

---

Instalar Pytorch

Esta es la ultima version de Pytorch que soporta Python 3.6

```bash
wget https://nvidia.box.com/shared/static/fjtbno0vpo676a25cgvuqc1wty0fkkg6.whl -O torch-1.10.0-cp36-cp36m-linux_aarch64.whl
```

```bash
sudo apt-get install libopenblas-base libopenmpi-dev libomp-dev
```

```bash
pip3 install 'Cython<3'
```

```bash
pip3 install numpy torch-1.10.0-cp36-cp36m-linux_aarch64.whl
```

La versión de Torchvision para este caso seria:

```bash
sudo -H pip3 install pillow
```

```bash
sudo apt-get install libjpeg-dev zlib1g-dev libpython3-dev libopenblas-dev libavcodec-dev libavformat-dev libswscale-dev
```

```bash
git clone --branch v0.11.1 https://github.com/pytorch/vision torchvision
```

```bash
export BUILD_VERSION=0.11.1
```

```bash
cd torchvision
```

```bash
python3 setup.py install --user
```

```bash
cd ../  # attempting to load torchvision from build dir will result in import error
```

```bash
pip install 'pillow<7' # always needed for Python 2.7, not needed torchvision v0.5.0+ with Python 3.6
```

Comprobar la instalación directamente en Python

```bash
import torch
print(torch.__version__)
print('CUDA available: ' + str(torch.cuda.is_available()))
print('cuDNN version: ' + str(torch.backends.cudnn.version()))
a = torch.cuda.FloatTensor(2).zero_()
print('Tensor a = ' + str(a))
b = torch.randn(2).cuda()
print('Tensor b = ' + str(b))
c = a + b
print('Tensor c = ' + str(c))

import torchvision
print(torchvision.__version__)
```

---

Instalar Numpy

```bash
sudo pip3 install --verbose numpy==1.19.5
```

---

Instalar Pandas

```bash
sudo pip3 install --verbose pandas==1.1.5
```

---

Instalar CuPy (Casi 2 horas)

```bash
sudo pip3 install --verbose cupy==9.2.0
```

---

Install Scikit-learn 0.24

```bash
sudo -H pip3 install scikit-learn==0.24.2
```

---

Install SciPy 1.5.4

```bash
sudo -H pip3 install scipy==1.5.4
```

---

Install Virtual Enviroment on Python

```bash
sudo apt-get install python3-venv
```

---

Install Virtual JupyterLab

```bash
pip3 install jupyterlab==2.2.9
```

---

Install Onnx

```bash
sudo -H pip3 install --verbose onnx==1.11.0
```

---

Instalar GO en ARM

Esta parte es completamente opcional, instalar GO y puede ser una guía genérica para instalar este lenguaje de programación que desafortunadamente no tiene soporte con CUDA a pesar de funcionar muy eficientemente.

Lo primero es ubicarse en una carpeta temporal como Downloads:

```bash
sudo reboot
```

```bash
cd Downloads
wget https://go.dev/dl/go1.23.5.linux-arm64.tar.gz
```

Extraemos el paquete:

```bash
sudo tar -C /usr/local -xzf ./go1.23.5.linux-arm64.tar.gz
```

Añade la ruta a go en tu archivo .bashrc.
Bash

```bash
echo 'export PATH="$PATH:/usr/local/go/bin"' >> ~/.bashrc
source ~/.bashrc
```

Para verificar la instalación ejecutamos:

```bash
go version
```

Finalmente se deberá obtener la salida como esta para asegurarnos de que se instaló correctamente:

go version go1.23.5 linux/arm64
