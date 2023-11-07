
Es un protocolo para que una aplicación le de accesso a sus datos a otra aplicación. Los accesos se dan a través de **tokens de autenticación**.

## JWT
Es un estandar, tiene su propio RFC. Y lo que resuelve JWT es el de tener que almacenar una referencia a los tokens que están afuera para que cuando lleguen los podamos identificar con un usuario. Esto quiere decir, que me llega un código y JWT resuelve a que usuario le pertenece ese código.

El token debe ser capaz de almacenar la información del usuario y además tiene que ser capaz de que nadie pueda modificar ese token en el camino y hacerse de autenticacion sólo porque sí. Y en la BD no hay que guardar referencia a ellos.

**JWT** lo que ofrece es un conjunto de datos conformado por firma criptográfica y algoritmo que usa. 

Partes de un **JWT**. La página muestra el mismo token codificado y decodificado:
- **HEADER (Algotithm an Token Type):**
- **Payload:**
- **Signature:**

Antes de usarlo, verificar en la página oficial las librerías porque hay muchas malas implementaciónes.