## Clases de IP
Las direcciones se dividen en clases, dependiendo de los bits por los que empieza el primer octeto de la dirección. Además cada clase tiene una máscara de red por defecto, esto quiere decir que por defecto utiliza cierto número de bits de la IP para el ID de red y los restantes para los hosts. 

| Clase            | Bits  Iniciales | Rango                        | Máscara por defecto | Bits de red | Bits de host |
| ---------------- | --------------- | ---------------------------- | ------------------- | ----------- | ------------ |
| A                | 0               | 0.0.0.0 a  127.255.255.255   | 255.0.0.0           | 8           | 24           |
| B                | 10              | 128.0.0.0 a  191.255.255.255 | 255.255.0.0         | 16          | 16           |
| C                | 110             | 192.0.0.0 a  239.255.255.255 | 255.255.255.0       | 24          | 8            |
| D (Multicast)    | 1110            | 224.0.0.0 a 239.255.255.255  |                     |             |              |
| E (Experimental) | 1111            | 240.0.0.0 - 255.255.255.254  |                     |             |              |

Las clases D y E no se utilizan normalmente, no es necesario que las aprendas, realmente con recordar esto es suficiente:

| Clase | Primer byte (en decimal) | Máscara por defecto |     |
| ----- | ------------------------ | ------------------- | --- |
| A     | 0 a 127                  | 255.0.0.0 (/8)      |     |
| B     | 128 a 191                | 255.255.0.0 (/16)   |     |
| C     | 192 para adelante        | 255.255.255.0 (/24) |     |

### Subredes
**Es posible, teniendo determinada IP perteneciente a un rango, aumentar el número de bits que se utilizan para la red**, creando de esta manera subredes. 
Aunque no vayamos a ver subredes en profundidad por el momento **es importante saber que debido a esto podemos tener direcciones IP que por el rango en el que se encuentran (por sus bits iniciales), sepamos que pertenece a una clase pero sin embargo tenga una máscara mayor, es decir, con más bits de red, pero nunca menor**, en ese caso no sería una dirección válida, se dice que no es congruente la máscara con la dirección.

El ejercicio que traías de ejemplo ya te daban la máscara junto con la IP, en lugar de decirte que utilices la por defecto de su rango, esto significa que la IP que te están dando pertenece a una subred.

Aquí te dejo un ejemplo sencillo de como se forma una subred, no para que lo aprendas ya que no te lo piden, pero puede ayudar a entender como funciona esto y de donde vienen estas direcciones que te dan:

Pongamos que tenemos asignada una IP privada 130.60.0.0 a nuestra red. Esta red como podemos comprobar por el rango en el que se encuentra es de clase B, si la ponemos en binario podemos comprobar que los bits iniciales también coinciden con los que se muestran el la tabla:
**10**00 0010 . 0011 1100 . 0000 0000 .0000 0000
*No necesitamos convertirlo a binario para saber a que clase pertenece, con ver que coincide en el rango nos llega ya que una cosa implica la otra, aquí lo hago para que se vea más claro*

Como sabemos la clase de la dirección podemos mirar en la tabla cual es su máscara, en este caso es /16

| IP      | **10**00 0010 . 0011 1100 . 0000 0000 . 0000 0000 |
|---------|---------------------------------------------------|
| Máscara | 1111 1111 . 1111 1111 . 0000 0000 . 0000 0000     |

Tenemos 16 bits de host, esto significa que tenemos una red a la que podríamos conectar, restando las direcciones reservadas para el id de red y la de broadcast:
2^16 - 2 = 65534 hosts
El rango de la red será de 130.60.0.0 a 130.60.255.255, incluyendo las direcciones de id y broadcast.

Pero es posible que, por ejemplo por temas de seguridad, queramos dividir nuestra red en redes distintas, para esto lo que hacemos es asignar más bits de la IP al id de red, es decir, aumentar el tamaño de la máscara de red.

Si aumentamos un bit la máscara de red dividiremos nuestra red en dos subredes, siguiendo con el ejemplo con la IP 130.60.0.0:

| IP                  | **10**00 0010 . 0011 1100 . 0000 0000 . 0000 0000 |
|---------------------|---------------------------------------------------|
| Máscara por defecto | 1111 1111 . 1111 1111 . 0000 0000 . 0000 0000     |
| Nueva máscara       | 1111 1111 . 1111 1111 . 1000 0000 . 0000 0000     |

De esta forma se nos crearían dos subredes, una en la que el nuevo bit es 0 y otra en la que el nuevo bit es 1, ambas con máscara /17, cada una ocupará la mitad de las direcciones que ocupaba la red inicial.
subred 1:

| IP            | **10**00 0010 . 0011 1100 . **0**000 0000 . 0000 0000 |
|---------------|-------------------------------------------------------|
| Máscara       | 1111 1111 . 1111 1111 . **1**000 0000 . 0000 0000     |
| IP en decimal | 130.60.0.0/17                                         |

subred 2:

| IP            | **10**00 0010 . 0011 1100 . **1**000 0000 . 0000 0000 |
|---------------|-------------------------------------------------------|
| Máscara       | 1111 1111 . 1111 1111 . **1**000 0000 . 0000 0000     |
| IP en decimal | 130.60.128.0/17                                       |


Como ves la IP de la primera subred coincide con la de la red que dividimos, pero con la máscara a /17, esto implica que empezará donde empezaba la red de la que partíamos pero solo llegará hasta la mitad, es decir su rango irá de 130.60.0.0 a 130.60.127.255, y la segunda cubrirá la otra mitad, de 130.60.128.0 a 130.60.255.255.

Entonces cuando en un ejercicio te dan una Ip con una máscara que no es la por defecto esto es lo que está ocurriendo, por ejemplo podrían darte la IP 130.60.240.120/17, que estaría dentro de la segunda subred que creamos.

Ahora realizaremos este ejercicio como hacemos siempre pero teniendo en cuenta las subredes:

## Ejercicio de ejemplo teniendo en cuenta subredes

130.60.240.120/17

| IP      | 1000 0010 . 0011 1100 . 1111 0000 . 0111 1000 |
|---------|-----------------------------------------------|
| Máscara | 1111 1111 . 1111 1111 . 1000 0000 . 0000 0000 |

Sustituimos por 0 los bits en la IP que coinciden con los 0 de la máscara (and) y obtenemos el id de la red:
1000 0010 . 0011 1100 . 1000 0000 . 0000 0000
en decimal: 130.60.128.0/17 que como vemos coincide con la segunda subred que creamos. 
Si no tenemos en cuenta subredes simplemente diríamos que este es el id de la red, aunque realmente es el de la subred. 
Para obtener el id de la red simplemente tenemos que hacer lo mismo pero utilizando la máscara por defecto para esta clase de IP, en este caso /16:

| IP        | 1000 0010 . 0011 1100 . 1111 0000 . 0111 1000 |
|-----------|-----------------------------------------------|
| Máscara   | 1111 1111 . 1111 1111 . 0000 0000 . 0000 0000 |
| Id de red | 1000 0010 . 0011 1100 . 0000 0000 . 0000 0000 |

y nos quedaría el id 130.60.0.0/16, que como vemos coincide con la dirección de la red de la que partíamos. Teniendo en cuenta esto, ahora, los bits de red de una los podemos dividir en bits de red y bits de subred. Los bits de red serían los que coinciden con la máscara de red y los de subred el resto hasta llegar a la máscara de la subred.

![](C:\Users\jotaj\Desktop\redes\bitsSubred.png)

