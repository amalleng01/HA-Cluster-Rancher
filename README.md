# Como hacer un cluster de Raspberries Pi de alta disponibilidad con Rancher
## Material que he usado para este proyecto 📋
He usado 2 Raspberry Pi 4B de 4GB de RAM con 64GB de MicroSD.
El resto de máquinas son virtualizadas.

## Puesta en marcha 🚀
Para comenzar has de tener clara la topología logíca que tendrá el cluster. En mi caso he usado la siguiente:
![tología-lógica](https://rancher.com/docs/img/rancher/k3s-architecture-ha-server.png)

Se pueden identificar partes importantes en esta arquitectura. Como los servidores rancher servers y agentes. Los servidores rancher, conocidos como maestros serán los encargados de administrar la carga de trabajo del cluster. Y la carga de trabajo será colocada por los maestro en los agentes, también conocidos como trabajadores o esclavos.
Por otra parte está la base de datos. En esta arquitectura es externa. Posteriormente hablaremos de la importancia de la base de datos y otras opciones.
Para terminar vemos el balanceador de cargas. Que tiene dos funciones, repartir las peticiones a los servidores maestros haciendo que sea de alta disponibilidad y poder hacer que los servicios en un futuro puedan ser expuestos al público.

## Topología de red 🖇️
Si estas hosteando todas las máquinas en tu casa, como mi caso. Sería interesante crear una DMZ, pero si no dispones de tantas tarjetas de red para poder crearla no pasa nada. Al fin y al cabo es un entorno de prueba. En el caso de que hostees las máquinas en la nube no tienes que preocuparte por crear la DMZ.

## Elementos y software ⚙️
Una vez conoces por encima los elementos, antes de empezar con la instalación y configuración de estos vamos a hablar en profundidad de cada uno.

* - Base de datos
* - Balanceador de cargas
* - Servidores maestros
* - Servidores esclavos

### Base de datos
La base de datos externa de nuestro cluster almacenará el estado de todos los pods de este. Es por eso que es uno de los elementos más importantes. Al ser una base de datos no tenemos redundancia, en el caso de que la base de datos "muera" no hace falta que diga lo que pasa acontinuación... Es por eso que una solución a esto sería crear la base de datos de alta disponibilidad con etcd en todas las máquinas maestro del cluster. Pero aquí no veremos esa arquitectura.

### Balanceador de cargas
El balanceador de cargas es el primer elemento que proporciona el acceso al cluster. Cuando recibe una petición, este la distribuirá por cualquiera de los servidores maestros del cluster indicados. Gracias a este podrás exponer al exterior y acceder a cualquier servicio del cluster.

### Servidor maestro y trabajador

![arquitectura-k3s](https://it.baiked.com/wp-content/uploads/2019/04/a0393e038e774a18a79b0b8c2240f466.jpeg)

## Instalación




