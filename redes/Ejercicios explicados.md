# Ejercicio 1
Dada la dirección IP: 145.167.210.53/19:
1. Expresar la máscara de red en decimal y en binario.
2. Identificar Bits de Red y Bits de Host de la IP.
3. Expresar, en decimal, el ID de la red.
4. Calcular el número de hosts que podremos tener conectados a esta red.
## Apartado 1
El enunciado nos indica que la máscara de red es /19, por lo tanto, su representación en binario serán 19 unos, seguido de 13 ceros.
1111 1111 . 1111 1111 . 1110 0000 . 0000 0000
Los escribimos separados por octetos (bytes) y convertimos cada octeto por separado al decimal:
255.255.224.0
## Apartado 2
Puesto que la máscara es /19 sabemos que los primeros 19 bits de la IP serán de red y los siguientes 13 de host, por lo tanto solo tenemos que pasar la dirección IP a binario e indicarlo. Para hacerlo más claro es posible colocar la mascara de red debajo en formato binario:

145.167.210.53/19

|         | Bits de red (19)            | Bits de host (13)  |
|---------|-----------------------------|--------------------|
| IP      | 1001 0001 . 1010 0111 . 110 | 1 0010 . 0011 0101 |
| Máscara | 1111 1111 . 1111 1111 . 111 | 0 0000 . 0000 0000 |
## Apartado 3
Como explicamos en la teoría el id de red es la primera IP dentro de una red, es decir, la que tiene todos sus bits de host a 0, por lo tanto, solo tenemos que coger la dirección IP en binario que ya convertimos en el paso anterior y sustituir sus bits de host a 0.

|           | Bits de red (19)            | Bits de host (13)  |
| --------- | --------------------------- | ------------------ |
| IP        | 1001 0001 . 1010 0111 . 110 | 1 0010 . 0011 0101 |
| Máscara   | 1111 1111 . 1111 1111 . 111 | 0 0000 . 0000 0000 |
| Id de red | 1001 0001 . 1010 0111 . 110 | 0 0000 . 0000 0000 |

Lo convertimos a decimal, de nuevo convirtiendo cada octeto por separado:
145.167.192.0
## Apartado 4
Utilizamos la fórmula que explicamos en la teoría: 2^n - 2, siendo n el número de bits de host. Por lo tanto: 2^13 - 2 = 16384 - 2 = 16382