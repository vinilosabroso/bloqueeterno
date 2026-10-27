# Bloque Eterno

Un puzzle de bloques 8×8 al estilo Block Blast, para jugar tranquilo: el generador de piezas lee el tablero y **nunca te deja sin jugada**.

## Jugar

Abrí `index.html` en el navegador (un solo archivo, sin dependencias). Arrastrá las piezas al tablero; las filas y columnas completas se limpian.

## Cómo garantiza que no perdés

1. **Cada tanda de 3 piezas** se valida con backtracking: existe al menos un orden y ubicación para colocar las tres, contando las líneas que se limpian en el camino. En modo *Asistido* elige, entre varias tandas válidas, la que mejor encaja en el tablero.
2. **Después de cada jugada**, si las piezas que quedan ya no tienen salida, se reemplaza la mínima cantidad necesaria (marcada como "rescate").
3. Un tablero 8×8 nunca puede quedar lleno (toda fila completa se limpia), así que el 1×1 siempre entra como último recurso.
