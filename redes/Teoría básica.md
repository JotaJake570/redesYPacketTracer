# Estructura de las direcciones IP
Las direcciones IP se utilizan para designar una red o subred; o un equipo (host) en concreto.  Cada dirección está formada por 4 bytes, que se escriben separados por un punto. Cada byte está formado por 8 bits, por lo que también es común llamarlos octetos. Estas direcciones, habitualmente son presentadas en formato decimal o en formato binario y se puede convertir de uno al otro convirtiendo cada byte por separado.

El formato binario es con el que trabajan los ordenadores a nivel lógico para hacer sus cálculos, el formato decimal es utilizado generalmente para hacer que sea más legible para los humanos y facilitar la introducción de los datos por estos al configurar los equipos.

Cada dirección IP utiliza un número de sus bits para indicar la red a la que pertenece y el resto para indicar el equipo en concreto (host) al que pertenece (excepto las direcciones especiales de id de red y broadcast que veremos más adelante). El número de bits que se utiliza para la red y para el host nos lo indica su máscara de red asociada.
# Máscaras de red
Cada dirección IP tiene una máscara de red asociada. Esta máscara, al igual que la IP, está formada por 4 bytes y también puede representarse tanto en binario como en decimal. Como se explicó en el apartado anterior indica que bits de una IP indican la red y cuales el host.
Si convertimos una máscara de red a binario siempre nos quedará una tira de unos seguida de una tira de ceros, por ejemplo:
255.255.192.0
1111 1111 . 1111 1111 . 1100 0000 . 0000 0000

Una máscara que no siga este formato, por ejemplo:
231.124.85.0
1110 0111 . 0111 1100 . 0101 0101 . 0000 0000
no sería válida.

El número de unos nos indicará cuantos bits pertenecen al id del red, el resto pertenecerán al host.
Debido a esto es habitual indicar la máscara de red junto a la IP, escribiendo tras la IP  una barra con un número, por ejemplo 192.168.0.0/25, esto nos indicaría que su máscara de red esta formada por 25 unos, y el resto (7) serían ceros:
1111 1111 . 1111 1111 . 1111 1111 . 1000 0000
en decimal:
255.255.255.128
## Utilización de la máscara de red
#### Obtención de los bits de red y los bits de host
Como explicábamos la máscara de red nos indica cuantos bits de la dirección pertenecen a la red y cuantos al host, por lo tanto si nos proporcionan esta dirección:
145.124.136.35/18, sabemos que sus 18 primeros bits indicarán la red y los 14 restantes el host. 
Si pasamos la IP 145.124.136.35 a binario y colocamos debajo su máscara de red expresada en binario (18 unos seguidos de 14 ceros), podemos distinguir que bits pertenecen a la red (los que coinciden con el 1 en la máscara) y cuales al host (los que coinciden con el 0):
![](C:\Users\jotaj\Desktop\redes\ej1.png)
Realmente no es necesario escribir la máscara en binario, nos llega con contar los primeros 18 bits de la dirección, pero colocando la máscara debajo se ve más claro.
## ¿Pero qué significan los bits de red y los bits de host?
Dentro de una misma red, las IPs de todos los equipos conectados compartirán los mismos bits de red, es decir, esa parte de la dirección será igual, pero cada equipo tendrá unos bits de hosts distintos, que lo identifican dentro de la red.

Por ejemplo, si tenemos una red con máscara /24, cuyos bits de red sean:
1001 0001 . 0111 1100 . 1000 1000
, los equipos conectados a esta red podrían tener las Ips:

| Bits de red (24)                    | Bits de host (8) |
|-------------------------------------|------------------|
| 1001 0001 . 0111 1100 . 1000 1000 . | 0000 0001        |
| 1001 0001 . 0111 1100 . 1000 1000 . | 0000 0010        |
| 1001 0001 . 0111 1100 . 1000 1000 . | 0000 0011        |
| 1001 0001 . 0111 1100 . 1000 1000 . | ...              |
| 1001 0001 . 0111 1100 . 1000 1000 . | 1111 1110        |
# Id de red
Como acabamos de ver dentro de una red las IPs de los equipos comparten bits de red pero sus bits de host son distintos. Dentro de cada red, reservamos la primera posición, es decir, en la que todos los bits de host están a 0 para el Id de red, esta dirección especial se utiliza para identificar al conjunto de la red, no se le asigna a ninguno de los host que tenga conectados.
## Calcular el Id de la red teniendo una IP y su máscara
Realizaremos el ejemplo utilizando la misma dirección que en el ejemplo de obtener los bits de red y host: 145.124.136.35/18

Primero utilizamos la máscara de red para saber que bits de la IP pertenecen a la red y cuales al host.

|         | Bits de red (18)           | Bits de host (14)   |
|---------|----------------------------|---------------------|
| IP      | 1001 0001 . 0111 1100 . 10 | 00 1000 . 0010 0011 |
| Máscara | 1111 1111 . 1111 1111 . 11 | 00 0000 . 0000 0000 |
Como habíamos comentado el Id de la red es la que tiene todos los bits de host a 0, entonces simplemente tenemos que sustituir los bits de hosts por ceros en nuestra dirección:

|           | Bits de red (18)           | Bits de host (14) |
|-----------|----------------------------|-------------------|
| Id de red | 1001 0001 . 0111 1100 . 10 | 00 0000 . 0000    |
Y este sería el Id de red, podemos convertir a decimal y nos quedaría:
145.124.128.0

# Dirección de broadcast
Al igual que la dirección de red, existe otra dirección especial en la red para broadcast, esta se utiliza para transmitir información a diferentes equipos dentro de una red a la vez. La dirección reservada para esta es la última de la red, es decir, la que tiene todos los bits de host a 1.

Si necesitamos calcularla podemos hacerlo igual que para el Id de red, simplemente estableciendo los bits de host a 1 en lugar de a 0.
# Calcular número de hosts que permite una red
Como explicamos anteriormente, dentro de una misma red, las IPs de todos los hosts tienen los mismos bits de red, pero sus bits de host varían, teniendo cada uno unos bits de host diferentes que lo identifican dentro de la red.
Por lo tanto, el número de hosts que podremos tener en una red estará delimitado por la cantidad de combinaciones posibles de 1s y 0s que podamos hacer con los bits de host. 
Por ejemplo si tenemos un solo bit de host, solo habrá dos posibilidades, que ese bit valga 0 o 1, si tenemos dos bit de hosts, las opciones serán 00, 01, 10 y 11.

En general cada bit de host que añadimos multiplica por dos las opciones anteriores, ya que las nuevas opciones posibles serán todas las que ya había, con un 0 o con un 1 delante, por lo tanto la fórmula que nos permite saber cuantas combinaciones hay con un número n de dígitos binarios es 2^n.
## Recuerda las direcciones de red y de broadcast!!!
Como hemos explicado dentro de cada red se reserva la primera dirección para el id de red y la última para broadcast, por lo tanto, al número de combinaciones posibles con los bits de host tenemos que restarle 2.
De esta forma la fórmula final para obtener los hosts posibles en una red sería
### (2^n) - 2
\* Las paréntesis no son necesarias, pero es necesario recordar que la potencia tiene prioridad ante la suma.

Debido a esto en la práctica nunca se utilizan máscaras superiores a 30.
### Ejemplo
Nos dan la IP 145.124.136.35/18 y nos piden calcular el número de hosts posibles.
Por su máscara sabemos que tiene 18 bits de red, por lo tanto el resto, 14, serán los bits de host.
Utilizamos la fórmula anterior:
2^14 - 2 = 16384 - 2 = 16382 hosts