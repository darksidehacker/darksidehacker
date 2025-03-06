---
layout: post
title: Containers Guide for Jetson Nano
date: 2025-02-18 15:09:00
description: Explain a Containers on Jetson Nano
tags: Jetson Software
categories: Work
featured: false
related_posts: false
---

Según <a href="https://es.wikipedia.org/wiki/Contenedor"> Wikipedia</a>, un contenedor es un recipiente de carga para el transporte marítimo. El objetivo de este es aislar y proteger las mercancias durante su traslado para que lleguen a su destino sin sufrir ningun tipo de daño para su uso o consumo. Y supongo que es el motivo por el cual tambien se le llama asi en el contexto de la computación, creo que no existe mejor definición que esta.

Un contenedor de aplicaciones, es una unidad de estándar de software en la que podemos empaquetar código con todas sus dependencias de forma aislada del sistema operativo anfitrion, lo que permite poder ejecutar este mismo codigo en otro sistema que soporte la tecnologia de contenedores, independientemente del entorno subyacente. Por esta razon las imágenes de los contenedores pueden reutilizarse para transportarse y desplegarse en otros entornos. Algo muy similar a una maquina virtual pero sin los altos consumos de CPU y RAM que esto puede traer, utilizando unos pocos MB de RAM. <a href="https://docs.docker.com/">Docker</a> es el estandar en la industria y su codigo fuente esta escrito en <a href="https://go.dev/">GO</a>.

¿Cuales son las ventajas?
Mi respuesta:
1.- Los contenedores y las maquinas virtuales se parecen demasiado. Sin embargo, mientras una maquina virtual requiere procesadores y memoria ram dedicada un contenedor solo requiere unos pocos MB de memoria para que pueda ser utilizado.
2.- Podemos crear y desplegar las aplicaciones a una nueva ubicación, como otra jetson nano.
3.- Si arruinamos las cosas dentro del contenedor simplemente puedes borrarlo e instalarlo de nuevo.
4.- Nvidia proporciona algunos contenedores que son de gran utilidad ya que ahorramos tiempo en la instalación de dependencias y estan listos para usarse.
5.- Ya viene preinstalado!

Este post pretende ser una guia basica enfocado al uso de arquitecturas ARM como lo es la Jetson Nano.
Si quieren explorar mas a fondo dejo estos enlaces.

- <a href="https://github.com/dusty-nv/jetson-containers?tab=readme-ov-file">Jetson Containers </a>
- <a href="https://catalog.ngc.nvidia.com">Catalogo NGC</a>(Contiene algunos contenedores de utilidad)
- <a href="https://docs.nvidia.com/deeplearning/frameworks/user-guide/index.html">Containers for Deep Learning Frameworks</a>

Los comando basicos de Docker son:

- Descargar una imagen

```c++
docker pull <nombre_de_la_imagen>
```

- Ejecutar el contenedor

```c++
docker run <nombre_de_la_imagen>
```

Existen muchas opciones para el comando run, por ejemplo:

```c++
-it
```

```c++
-d
```

```c++
-p
```

```c++
-v
```

Listar contenedores en ejecucion

```c++
docker ps
```

Listar todos los contenedores

```c++
docker ps -a
```

Detener el contenedor

```c++
docker stop
```

Eliminar un contenedor

```c++
docker rm <id_del_contenedor>
```

Eliminar una imagen:

```c++
docker rmi <id_de_la_imagen>
```


Y ahora para aplicar todo lo que vimos en concreto, aqui un ejemplo tomado del catalogo NGC.

Obtener la imagen JetPack-L4T, la última disponible para hacer ML en la Jetson Nano

```c++
sudo docker pull nvcr.io/nvidia/l4t-ml:r32.7.1-py3
```

Eliminar una imagen:

```c++
sudo docker run -it --rm --runtime nvidia --network host nvcr.io/nvidia/l4t-ml:r32.7.1-py3
```

Si queremos montar directorios desde el host

```c++
sudo docker run -it --rm --runtime nvidia --network host -v /home/user/project:/location/in/container nvcr.io/nvidia/l4t-ml:r32.7.1-py3
```
