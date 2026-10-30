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

## Coach
Lee el historial a medida que guardás partidas del Tutor y entrena tus falencias.

- **Motor con mirada a futuro**: además de las líneas, valora la probabilidad de que la próxima pieza al azar tenga lugar (según la frecuencia real de cada pieza) y castiga más los huecos, porque el Punto casi no sale. En partidas simuladas con las mismas tandas, seguir al motor necesita ~17% menos rescates que la versión anterior.
- **Causa de cada error**: huecos aislados, sin lugar para el 3×3, espacio fragmentado, bordes irregulares, líneas que dejaste pasar, romper líneas a cualquier costo y orden de las piezas.
- **Diagnóstico y foco**: con 3 partidas medibles (sin pistas ni avisos) y 60 jugadas, rankea tus falencias por costo cada 100 jugadas y elige una como foco. Se da por superado cuando baja 30% o más en al menos 3 partidas.
- **Ejercicios**: tableros reales donde te equivocaste, con repetición espaciada (1, 3, 7 y 21 días). Primero los de tu foco.
- **Avisos dirigidos**: durante el arrastre, solo cuando estás por cometer el error de tu foco.
- **Reporte para Claude**: un `.md` con instrucciones y datos en JSON, para pegar en una conversación y pedir un diagnóstico.
- **Puntos por vida**: puntos sumados entre rescates en cada partida del Tutor (la última vida termina cuando cerrás la partida, no por perder).
- **Errores sin causa clara**: registro persistente (no se borra con el historial, hasta 400 casos) con tablero, bandeja, tu jugada, la sugerida, el mejor final de la bandeja en cada caso, métricas comparadas y qué pasó en las jugadas siguientes. Se exporta con su propio prompt para que Claude proponga reglas nuevas o detecte errores del motor.
