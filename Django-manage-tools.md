## manage.py
Al ejecutar en terminal solo:
```Shell
user@machine~$ python manage.py
```
Aparecen todos los scripts que se pueden ejecutar usando `manage.py`, entre los scripts hay herramientas que sirven para levantar el proyecto, para crear las migraciones o para debuguear el proyecto.

#### **shell_plus**
Esta en `[django_extensions]`, y se ejecuta `python manage.py shell_plus`.
En primera instancia hace los imports automáticamente, tanto libs del proyecto como modelos del proyecto. Y se habilita la consola para como para ir consultantdo cosas, por ejemplo:
```python
In [1]: NombreDeModelo.object.all()
```
