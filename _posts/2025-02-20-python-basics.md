---
layout: post
title: Python Basics
date: 2025-02-20 05:57:00-0400
description: Python Basics
tags: Jetson Python
categories: Work
giscus_comments: true
related_posts: false
---

Dejo una pequeña introducción de Python desde tipos de datos hasta slices.
Mas a

{::nomarkdown}
{% assign jupyter_path = "assets/jupyter/learn_python.ipynb" | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/blog.ipynb %}{% endcapture %}
{% if notebook_exists == "true" %}
{% jupyter_notebook jupyter_path %}
{% else %}

<p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}

Note that the jupyter notebook supports both light and dark themes.
