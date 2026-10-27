# Bloque Eterno

Puzzle de bloques 8×8 al estilo Block Blast, en un solo archivo (`index.html`, sin dependencias). Dos modos:

## Eterno
El generador lee el tablero y **nunca te deja sin jugada**:
1. Cada tanda de 3 se valida con backtracking (existe un orden y ubicación para colocar las tres, contando las líneas que se limpian). Entre varias tandas válidas elige la que mejor encaja.
2. Si una jugada deja al resto de la tanda sin salida, cambia la mínima cantidad de piezas ("rescate").
3. Un 8×8 nunca puede quedar lleno (toda fila completa se limpia), así que el 1×1 siempre entra.

## Tutor
Tandas **aleatorias reales**, como el juego original, con red de rescate solo cuando el juego real terminaría ("vida salvada").

- **Evaluación de cada jugada**: se compara con la mejor posible usando solo lo que veías (tablero + piezas de la tanda). La salud del tablero premia espacio libre y lugar para el 3×3, y castiga huecos aislados y bordes irregulares. Clasificación: óptima / buena / imprecisa / error, y detecta errores de orden.
- **Pistas en vivo** (desactivables): marca la mejor pieza para empezar y la mejor posición mientras arrastrás.
- **Balance** al terminar: puntaje global (Decisiones 50%, Supervivencia 20%, Orden 15%, Salud del tablero 15%; los puntos del juego no entran), distribución de jugadas, vidas salvadas, errores de orden, huecos, falta de lugar para el 3×3, pieza problemática, precisión 1ª vs 2ª mitad y repetición de la peor jugada.
- **Historial** con fecha: tendencia, patrones (mejora, pieza más difícil, cansancio, momento del día) y tabla de partidas. Se guarda en el navegador; "Copiar historial" / "Importar" para pasarlo entre dispositivos.
