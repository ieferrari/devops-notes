#Objetivos:
    # crear el sitio rápido
    # mínima necesidad de mantenimiento:
        # panel apra edición de entradas tipo blog

#Instalación
~$ sudo pip3 install wagtail

#Nuevo proyecto
$ wagtail start new_wagtail_web
$ cd new_wagtail_web
$ ./manage.py migrate
$ ./manage.py createsuperuser
$ ./manage.py runserver

# además de iniciar un proyecto django:
    #crea una app:  home con sus models y tempaltes

#código de nombres:
    #home/models.py         class HomePage()
    #home/templates/home    home_page.html


# creo una página en home/models.py
from django.db import models
from wagtail.core.models import Page
from wagtail.core.fields import RichTextField
from wagtail.admin.edit_handlers import FieldPanel
class HomePage(Page):
    body = RichTextField(blank=True)
    content_panels = Page.content_panels + [FieldPanel('body'),]


#realizo las migraciones
$ ./manage.py makemitrations
$ ./manage.py migrate


# agrego la página desde el admin del navegador
http://127.0.0.1:8000/admin
Pages>>Pages>>add child page  >>titulo  >>body
#la pongo como página de inicio
settings>sites>localhost >>rootpage >>choose a new root page


#creo el html en home/templates/home/home_page.html
# a esta se le pasa el context(page) que se cargó en el admin
{% extends "base.html" %}
{% load wagtailcore_tags%}
{% block content %}
    <h1> {{page.title}}</h1>
    {{page.body|richtext}}
{% endblock content %}


#creo una app subpágina
$./mangage.py startapp <app>

#la agrego en installed apps en:
<project>/<project>/settings/base.py

#creo una pag en los <app>/models.py
