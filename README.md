**Organización de computadores**
**Proyecto 4 - Programación**
**2026-2**

# Ya denle la licencia a Pablo

Ayuda a Pablo a aprobar su examen de conducir sin chocar ningún carro.

# Integrantes

| Nombre | Usuario GitHub | Aportes principales |
|---|---|---|
| Laura Santamaria Espinosa | *(completar)* | *(completar)* |
| Pablo Alvarez Restrepo | *(completar)* | *(completar)* |

# Compilación y ejecución

1. Compilar la carpeta con el JackCompiler oficial:

   ```
   tools/JackCompiler.bat RUTA/proyecto4
   ```

2. Abrir `tools/VMEmulator.bat`, **File → Load Program**, elegir la carpeta `proyecto4` y aceptar el uso del sistema operativo interno.
3. Elegir **No animation**, velocidad máxima y **Run**. Hacer clic en la pantalla del emulador para usar el teclado.

Pruebas públicas (Git Bash): `./correr_pruebas.sh RUTA/proyecto4 RUTA/nand2tetris/tools`

# Controles

| Tecla | Acción |
|---|---|
| 1, 2, 3 | Elegir la distancia: 150, 300 o 600 pasos |
| ENTER | Empezar |
| Flecha arriba / abajo | Cambiar de carril |
| P | Pausar y continuar |
| R | Volver a la pantalla inicial |
| ESC | Salir |

# Diseño de clases

| Clase | Responsabilidad |
|---|---|
| `Main` | Crea el juego, lo ejecuta y lo libera. |
| `Juego` | Ciclo del juego: pantalla inicial, partida, pausa y final. Lee el teclado. |
| `Carrera` | Reglas: carro, vidas, puntaje, progreso, choques y generación de obstáculos. |
| `Obstaculo` | Un obstáculo: tipo, carril y columna. |
| `Vista` | Dibuja las pantallas, la vía, el carro, los obstáculos y el marcador. |
| `Sprites` | Los dibujos de 16 × 16 del carro, los obstáculos y las líneas de la vía. |

Los cuatro tipos de obstáculo usan la misma clase `Obstaculo`. El campo `tipo` define cómo es cada uno: `largo()` devuelve 3 para el camión y 1 para los demás, `velocidad()` devuelve 2 para la moto y 1 para los demás, y `esLetal()` es falso solo para la moneda. Así no hace falta una clase por tipo ni herencia.

`Carrera` y `Obstaculo` no usan `Screen`, `Output`, `Keyboard`, `Grafico` ni `Sys.wait`. `Juego` lee el teclado y llama a `Carrera` y a `Vista`; `Vista` solo lee la carrera para dibujarla.

En cada paso, `Vista.borrar` borra las celdas que los obstáculos van a dejar libres, `Carrera` avanza y genera, y `Vista.dibujar` dibuja solo los obstáculos, el carro y el marcador.

# Rutinas VM

| Función | Qué hace | Dónde se usa |
|---|---|---|
| `Grafico.dibujarCelda` | Copia las 16 líneas del sprite a la celda. | Carro, obstáculos y líneas divisorias (`Vista`). |
| `Grafico.borrarCelda` | Pone en blanco una celda. | Borrar obstáculos y el carro al cambiar de carril (`Vista`). |
| `Grafico.desplazarFila` | Mueve una fila de celdas una celda a la izquierda. | Las líneas divisorias, para dar sensación de movimiento (`Vista.dibujar`). |
| `Grafico.direccion` | Auxiliar: `16384 + fila*512 + col` usando sumas. | Las tres funciones anteriores. |
| `Aleatorio.semilla` / `Aleatorio.siguiente` | Generador `x = 5x + 3`. | Generación de obstáculos (`Carrera`). |

# Uso de IA

Se usó Claude (Anthropic) para generar el código Jack y VM, los sprites y el borrador de este README, a partir del enunciado y de nuestras indicaciones. *(Completar: qué revisaron, probaron o cambiaron ustedes.)*
