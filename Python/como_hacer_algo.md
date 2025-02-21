# Como hacer cosas
Instrucciones para agilizar las instalaciones, etc.

# Git
- Establecer nombre de branch por default `git config --global init.defaultBranch <name>`.
- Para renombrar la branch principal es `git branch -m <name>`
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com


# Instalar Node.js en Debian
1 - Descargar el archivo "tar.xz"
2 - Hacer un `sudo apt update`
3 - `sudo tar -xvf node-v20.15.0-linux-x64.tar.xz`. Si no se tienen las herramientas para descomprimir, descargarlas con `sudo apt install xz-utils`
4 - `sudo cp -r node-v20.15.0-linux-x64/{bin, includo,lib,share} /usr/`... y listo.
5 - Comprobar la version con `node --version`.

# Instalar Npm
1 - Después de instalar node.js, hacer `npm install npm`.
2 - Checkear la version con `npm --version`

# Instalar Vite [https://vitejs.dev/guide/]
1 - En el directorio `npm create vite@latest my-react-app -- --template react-ts`
2 - Entrar al proyecto
3 - `npm install`
4 - `npm run dev`

PROY$%git098   VINO**69tinto

# Pasos GitLab
cd existing_repo
git remote add origin https://gitlab.com/emetechlab/front-members.git
git branch -M main
git push -uf origin main

## Cambiar prompt en bash (terminal)
1 - Entrar por terminal, desde "Home": `vim .bashrc`
2 - En la linea donde tengo por ejemplo: `#PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$'`
    que se puede comentar con el "#".
3 - Reemplazar esa linea por otra generada por algun 'prompt generator' como el de [https://bash-prompt-generator.org/] por ejemplo:
    `PS1='\[\e[1m\]@\[\e[3m\]\u\[\e[23m\][\[\e[0m\]\w\[\e[1m\]]\[\e[0m\]_'`.
4 - Guardar y salir del editor
5 - luego se puede hacer un `source .bashrc` para actualizar y listo.

## uuid - Resumen de cada version

## git: [https://github.com/uuidjs/uuid#readme]
- **Version 1:** UUIDs using a timestamp and monotonic counter.
- **Version 3:** UUIDs based on the MD5 hash of some data.
- **Version 4:** UUIDs with random data.
- **Version 5:** UUIDs based on the SHA1 hash of some data.
- **Version 6:** UUIDs using a timestamp and monotonic counter (sortable).
- **Version 7:** UUIDs using a Unix timestamp (sortable).
- **Version 8:** UUIDs using user-defined data.

# Python

## Python
- Ver version python3 `python3 --version`.
- Instalar python `apt-get install python3 python3-dev`.
- Instalar python `apt install python3-xyz`.

## requirement.txt
1. Crear el archivo "requirements.txt"
2. Instalar con comando `pip install -r requirements.txt`

## Pip
- Instalar pip `sudo apt install python3-pip`.
- Ver version pip `python3 -m pip --version`.
- Ver cosas instaladas: `pip list`

## Entorno virtual
- Crear entorno virtual con el mismo python `python3 -m venv .env`.
- Entrar a la ubicación del entorno para activarlo `source .env/bin/activate`
-Una vez que active el entorno virtual ya puedo instalar todos los paquetes para dicho entorno.

## Fastapi
- Instalar `pip3 install fastapi`.
- Instalar el servidor para correr la api `pip3 install "uvicorn[standard]"`
- Instalar el servidor para correr la api `pip3 install "fastapi[standard]"`
- Arrancar Fastapi `fastapi dev main.py`
- Reload de Uvicorn `uvicorn main:app --reload`

*app = Fastapi()* es una instancia de Fastapi() y es a la que referimos cuando usamos'uvicorn'. Ej: `$ uvicorn main:app --reload`.
Si se cambia el nombre de la instancia, se cambia el comando. Ej:
*instancia_aplicacion = Fastapi()*
`uvicorn main:instancia_aplicacion --reload`

*Fastapi usa **SQLAlchemy** como un **ORM** y **psycopg2** como el **adapter**
**Leeer https://sqlmodel.tiangolo.com/**
**Leeer https://www.psycopg.org/**

Para instalar **psycopg** es `pip install psycopg`, pero tambien necesita `sudo apt install libpq5` (si uso debian).
Luego para ambientes productivos se podria usar `pip install "psycopg[binary]"` proque el otro tambien sirve para debuguear y esas cosas.

### Url
Serving at: http://127.0.0.1:8000 
Openapio: http://127.0.0.1:8000/openapi.json 
API docs: http://127.0.0.1:8000/docs 

### Standar de Fastapi para los métodos:
- POST: Crear datos
- GET: Leer datos
- PUT: Actualizar datos
- DELETE: Borrar datos

## Django
1. Crear una carpeta donde va a estar el proyecto y dentro crear un entorno virtual con: `python3 -m venv .env` (se activa con `$ source .env/bin/source`)
2. Instalar django: `python -m pip install Django`
2. Instalar cosas: `pip install django-ckeditor Pillow`
3. Ver version de django: `python -m django --version`
4. Ver admin de django: `python -m django help` o `django-admin help`
5. Crear proyecto django: `django-admin startproject nombre-proyecto`
6. Levantar django: `python manage.py runserver` o `python carpetaContenedora/manage.py runserver`.
   Levantar django en otro puerto: `python3 manage.py runserver 7000`, levanta en puerto '7000'.
8. Migrar BD: `python manage.py migrate`
9. Crear una **app**: `python manage.py startapp nombreApp`, luego agregar la app en **settings** y despues en **urls**

10. Despues de crear o modificar un *Modelo* hay que migrarlo con: `python manage.py makemigrations` y luego tirar un `python manage.py migrate` y `python manage.py migrate ubicacion`

11. Crear super usuario para el administrador: `python manage.py createsuperuser` y completar lo que pide (emi, emi@mail.com, 1234). Luego para entrar al administrador es en [http://127.0.0.1:8000/admin/]

### Django Rest Framework
1. Instalar django rest framework: [https://www.django-rest-framework.org/]
```bash
pip install djangorestframework
pip install markdown       # Markdown support for the browsable API.
pip install django-filter  # Filtering support
```
En la docu estan todos  los pasos, es mas largo el asunto

2. crear carpeta **api** que es donde metemos los *endpoints*

#### Django shell
obtener un modelo `modelo = Model.objects.get(pk=1)`
mostrar un valor en pantalla `modelo.values('dni')`

# Postgres
Ver conexion: `$ netstat -plnt`
Conexión con postgres (ingreso así nomás): `$ sudo -u postgres psql`
**Una vez que se ingresa al prompt de postgres, ya todas las instrucciones válidas son las de SQL, no admite otra. Ya sea para crear un usuario, darle permisos, crear DB, etc.**
Crear BD: `postgres=# CREATE DATABASE mydb;`
Crear usuario: `CREATE USER miuser WHIT PASSWORD 'contraseña';`

Para borrar DB: `DROP DATABASE productos;`
Resetear postgres: `sudo service postgresql restart`
Crear usuario: `CREATE USER emiadmin WITH PASSWORD 'contra';`

Permisos que necesita un usuario para escribir
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO emiadmin; 
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA productos TO emiadmin;

# Integración Mongo en Django

1. Instalar `pip install pymongo[snappy,gssapi,srv,tls]`
2.  install dnspython for using mongodb+srv:// URIs with the command: `pip install dnspython`
3.  Crear una session de mongo: (éste método puede ser usado en ./myfirstapp/view.py)
   ```python
    from pymongo import MongoClient
    def get_db_handle(db_name, host, port, username, password):
    
     client = MongoClient(host=host,
                          port=int(port),
                          username=username,
                          password=password
                         )
     db_handle = client['db_name']
     return db_handle, client
```
4. Obtener la conexión:
```python
    from pymongo import MongoClient
    client = MongoClient('connection_string')
    db = client['db_name']
```
Donde,
```python
 connection_string = mongodb+srv://<username>:<password>@<atlas cluster>
/<myFirstDatabase>?retryWrites=true&w=majority
```
Por ejemplo:
```python
    makemyrx_db = client['sample_medicines']
    #collection object
    medicines_collection = makemyrx_db['medicinedetails']
```
Para conectar localhost se puede usar: `MongoClient(‘localhost’, 27017)` o `MongoClient(‘mongodb://localhost: 27017/’)`.

5. MongoEngine (es el ORM). Conectar el motor de mongo "MongoEngine": `pip install mongoengine`.
Luego conectar el motor:
```python
    import mongoengine
    mongoengine.connect(db=db_name, host=hostname, username=username, password=pwd)
```

6. Djongo (es el ODM-Objet Document Mapping). Instalación: `pip install djongo`.
Agregarlo a "settings.py"
```python
     DATABASES = {
           'default': {
               'ENGINE': 'djongo',
               'NAME': 'db-name',
           }
       }
```
o,
```python
DATABASES = {
        'default': {
            'ENGINE': 'djongo',
            'NAME': 'your-db-name',
            'ENFORCE_SCHEMA': False,
            'CLIENT': {
                'host': 'mongodb+srv://<username>:<password>@<atlas cluster>/<myFirstDatabase>?retryWrites=true&w=majority'
            }  
        }
}
```
Luego se puede ejecutar: `python manage.py makemigrations <app-name>` y luego `python manage.py migrate`

7. Implementación:
```python
    import pymongo
    #connect_string = 'mongodb+srv://<username>:<password>@<atlas cluster>/<myFirstDatabase>?retryWrites=true&w=majority' 
    
    from django.conf import settings
    my_client = pymongo.MongoClient(connect_string)
    
    # First define the database name
    dbname = my_client['sample_medicines']
    
    # Now get/create collection name (remember that you will see the database in your mongodb cluster only after you create a collection
    collection_name = dbname["medicinedetails"]
    
    #let's create two documents
    medicine_1 = {
        "medicine_id": "RR000123456",
        "common_name" : "Paracetamol",
        "scientific_name" : "",
        "available" : "Y",
        "category": "fever"
    }
    medicine_2 = {
        "medicine_id": "RR000342522",
        "common_name" : "Metformin",
        "scientific_name" : "",
        "available" : "Y",
        "category" : "type 2 diabetes"
    }
    # Insert the documents
    collection_name.insert_many([medicine_1,medicine_2])
    # Check the count
    count = collection_name.count()
    print(count)
    
    # Read the documents
    med_details = collection_name.find({})
    # Print on the terminal
    for r in med_details:
        print(r["common_name"])
    # Update one document
    update_data = collection_name.update_one({'medicine_id':'RR000123456'}, {'$set':{'common_name':'Paracetamol 500'}})
    
    # Delete one document
    delete_data = collection_name.delete_one({'medicine_id':'RR000123456'})
```
