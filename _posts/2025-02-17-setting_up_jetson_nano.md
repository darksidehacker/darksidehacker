---
layout: post
title: Setting Up Jetson Nano Waveshare
date: 2025-02-17 15:09:00
description: Setting Up Jetson Nano Waveshare
tags: Jetson
categories: Work
featured: true
related_posts: false
giscus_comments: true
---

En esta publicación requiere de su ayuda para construir un setup con todas las dependencias instaladas para nuestra aplicacion especifica.

Mostrare los pasos empiricos que hemos seguido para la configuración de esta versión de la Jetson Nano de Waveshare, que nos ha generado muchos quebraderos de cabeza.

(He dejado abiertos los comentarios para que comenten cualquier hallazgo que encuentren y lo documenten)

- Instalar Virtual Box o <a href="https://knowledge.broadcom.com/external/article/344595/downloading-and-installing-vmware-workst.html"> VMWare WorkStation Pro </a>
- Crear una maquina virtual e instalar dentro de esta <a href="https://releases.ubuntu.com/18.04/">Ubuntu 18.04</a>
- Una vez creado y actualizado instalar <a href="https://developer.nvidia.com/sdk-manager">SDK Manager</a>
- Ejecutar SDK Manager y conectar la Jetson Nano.
- Asegurarse de que la maquina virtual reconozca el dispositivo USB
- Instalar unicamente el S.O. sin ningun complemento adicional.
