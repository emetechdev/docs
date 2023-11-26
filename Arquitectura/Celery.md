## Flower
Es una aplicación escrita en django que nos permite ver que procesos se están ejecutando. Para usarlo en el navegador requere usuario y contraseña que se configuran en local con las variables "CELERY_FLOWER_USER" y "CELERY_FLOWER_PASSWORD".
En la interfaz se pueden ver los brokers

## Celery
Se encarga de la administración de todas las tareas que tienen que suceder fuera de los procesos síncronos de django y hace eso a través de "Redis" como broker de mensajes, que tiene la parte de **Broker** que se encarga de pedir los mensajes de "Redis" y empezar a ejecutar las tareas. Y tiene los **Producers** que mandan a llamar esas tareas, empujan los mensajes a "Redis" para que despues los **Brokers** las ejecuten.
Implementar un sistema así, usualmente es complejo porque implica correr el **Broker**, correr **Celery** (que va a estar pidiendo los procesos) y a veces instalarlo entre diferentes plataformas suele ser tedioso.


## Tareas Periodicas
Son las que no están siendo llamadas por nadie pero se ejecuatan periodicamente