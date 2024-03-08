
### 10.123.240.5/10
###### Escribir la máscara en binario y en decimal
La máscara es /10, por lo tanto su representación en binario estará formada por 10 unos, que indicarán los bits de red, seguido de ceros hasta llegar a 32, es decir 22 ceros.

1111 1111 . 1100 0000 . 0000 0000 . 0000 0000

Tras escribirla separada en octetos convertimos a decimal cada uno por separado:

255.192.0.0
###### Escribir la IP en binario e identificar los bits de red y los bits de host
Convertimos la Ip a binario convirtiendo cada uno de los octetos por separado:
0000 1010 . 01111 011 . 1111 0000 . 0000 0101

Una vez tenemos la Ip en binario, como el enunciado indica que la máscara es /10 sabemos que los primeros 10 bits serán los de red y los 22 restantes los de host. También es posible colocar la máscara debajo de la IP y los bits de la IP que coincidan con los unos serán los de red y el resto los de host:

0000 1010 . 01111 011 . 1111 0000 . 0000 0101
1111 1111 . 1100 0000 . 0000 0000 . 0000 0000

De esta manera nos quedaría:

| Bits de red (10) | Bits de host (22)               |
| ---------------- | ------------------------------- |
| 0000 1010 . 01   | 11 1011 . 1111 0000 . 0000 0101 |

###### Escribir el ID de red, en binario y en decimal
Para obtener el Id de red simplemente necesitamos coger la Ip en binario que obtuvimos en el apartado anterior y establecer todos sus bits de host a cero:

|             | Bits de red (10) | Bits de host (22)               |
| ----------- | ---------------- | ------------------------------- |
| Ip original | 0000 1010 . 01   | 11 1011 . 1111 0000 . 0000 0101 |
| Id de red   | 0000 1010 . 01   | 00 0000 . 0000 0000 . 0000 0000 |
Lo convertimos a decimal:
10.64.0.0
###### Calcular el número de hosts máximo que permitirá esta red
Tenemos 22 bits de host, por lo tanto deberemos calcular todas las posibles combinaciones con estos dígitos y restarle 2 por las direcciones reservadas para ID de red y broadcast, la fórmula que sale es 2^n - 2, siendo n el número de bits de host, en este caso 22: 

2^22 - 2 = 4194304 - 2 = 4194302 hosts

###### Calcular el rango de direcciones que podrán utilizar los hosts
Todos los hosts tendrán los mismos bits de red, pero cada uno tendrá unos bits de host distintos, sabemos que la primera dirección, está reservada para el Id y la última para broadcast, entonces, el rango de direcciones que utilizarán los host irá desde la segunda hasta la penúltima.

La segunda dirección será la que tenga todos los bits de host a cero excepto el último.
La Penúltima dirección será la que tenga todos los bits de host a uno menos el último.

|                     | Bits de red (10) | Bits de host (22)               |
| ------------------- | ---------------- | ------------------------------- |
| Ip original         | 0000 1010 . 01   | 11 1011 . 1111 0000 . 0000 0101 |
| 2a dirección        | 0000 1010 . 01   | 00 0000 . 0000 0000 . 0000 0001 |
| Penúltima dirección | 0000 1010 . 01   | 11 1111 . 1111 1111 . 1111 1110 |
Si las transformamos a decimal:
2a dirección: 10.64.0.1
penúltima dirección: 10.127.255.254

Y este sería el rango de direcciones que utilizarán los hosts, de 10.64.0.1 a 10.127.255.254
### 185.134.210.11/19

###### Escribir la máscara en binario y en decimal
La máscara es /19, por lo tanto:

1111 1111 . 1111 1111 . 1110 0000 . 0000 0000

Tras escribirla separada en octetos convertimos a decimal cada uno por separado:

255.255.224.0
###### Escribir la IP en binario e identificar los bits de red y los bits de host
Convertimos la Ip a binario convirtiendo cada uno de los octetos por separado:
1011 1001 . 1000 0110 . 1101 0010 . 0000 1011

La comparamos con la máscara:
1011 1001 . 1000 0110 . 1101 0010 . 0000 1011
1111 1111 . 1111 1111 . 1110 0000 . 0000 0000

De esta manera nos quedaría:

| Bits de red (19)            | Bits de host (13)  |
| --------------------------- | ------------------ |
| 1011 1001 . 1000 0110 . 110 | 1 0010 . 0000 1011 |

###### Escribir el ID de red, en binario y en decimal
Para obtener el Id de red simplemente necesitamos coger la Ip en binario que obtuvimos en el apartado anterior y establecer todos sus bits de host a cero:

|             | Bits de red (19)            | Bits de host (13)  |
| ----------- | --------------------------- | ------------------ |
| Ip original | 1011 1001 . 1000 0110 . 110 | 1 0010 . 0000 1011 |
| Id de red   | 1011 1001 . 1000 0110 . 110 | 0 0000 . 0000 0000 |
Lo convertimos a decimal:
185.134.192.0
###### Calcular el número de hosts máximo que permitirá esta red
Tenemos 13 bits de host, por lo tanto, utilizando la fórmula 2^n - 2: 

2^13 - 2 = 8192 - 2 = 8190 hosts

###### Calcular el rango de direcciones que podrán utilizar los hosts

|                     | Bits de red (19)            | Bits de host (13)  |
| ------------------- | --------------------------- | ------------------ |
| Ip original         | 1011 1001 . 1000 0110 . 110 | 1 0010 . 0000 1011 |
| 2a dirección        | 1011 1001 . 1000 0110 . 110 | 0 0000 . 0000 0001 |
| Penúltima dirección | 1011 1001 . 1000 0110 . 110 | 1 1111 . 1111 1110 |
Si las transformamos a decimal:
185.134.192.1 a 185.134.223.254
### 195.120.80.41/29
###### Escribir la máscara en binario y en decimal
La máscara es /29, por lo tanto:

1111 1111 . 1111 1111 . 1111 1111 . 1111 1000

Tras escribirla separada en octetos convertimos a decimal cada uno por separado:

255.255.2555.248
###### Escribir la IP en binario e identificar los bits de red y los bits de host
Convertimos la Ip a binario convirtiendo cada uno de los octetos por separado:
1100 0011 . 01111 000 . 0101 0000 . 0010 1001

La comparamos con la máscara:
1100 0011 . 01111 000 . 0101 0000 . 0010 1001
1111 1111 . 1111 1111 . 1111 1111 . 1111 1000

De esta manera nos quedaría:

| Bits de red (29)                           | Bits de host (3) |
| ------------------------------------------ | ---------------- |
| 1100 0011 . 01111 000 . 0101 0000 . 0010 1 | 001              |

###### Escribir el ID de red, en binario y en decimal
Para obtener el Id de red simplemente necesitamos coger la Ip en binario que obtuvimos en el apartado anterior y establecer todos sus bits de host a cero:

|             | Bits de red (29)                           | Bits de host (3) |
| ----------- | ------------------------------------------ | ---------------- |
| Ip original | 1100 0011 . 01111 000 . 0101 0000 . 0010 1 | 001              |
| Id de red   | 1100 0011 . 01111 000 . 0101 0000 . 0010 1 | 000              |

Lo convertimos a decimal:
195.120.80.40
###### Calcular el número de hosts máximo que permitirá esta red
Tenemos 3 bits de host, por lo tanto, utilizando la fórmula 2^n - 2: 

2^3 - 2 = 8 - 2 = 6 hosts

###### Calcular el rango de direcciones que podrán utilizar los hosts

|                     | Bits de red (29)                           | Bits de host (3) |
| ------------------- | ------------------------------------------ | ---------------- |
| Ip original         | 1100 0011 . 01111 000 . 0101 0000 . 0010 1 | 001              |
| 2a dirección        | 1100 0011 . 01111 000 . 0101 0000 . 0010 1 | 001              |
| Penúltima dirección | 1100 0011 . 01111 000 . 0101 0000 . 0010 1 | 110              |
Si las transformamos a decimal:
195.120.80.41 a 195.120.80.46