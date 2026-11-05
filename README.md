# Proyecto-Academico-PonDimension3D
# 🏓 Pong Dimension 3D

> Videojuego de pin-pong en 3D con física de rebote, cámara dinámica e inteligencia artificial.

![Unity](https://img.shields.io/badge/Motor-Unity%203D-black?logo=unity)
![C#](https://img.shields.io/badge/Lenguaje-C%23-239120?logo=csharp)
![Estado](https://img.shields.io/badge/Estado-Dise%C3%B1o%20y%20prototipo-orange)
![Plataforma](https://img.shields.io/badge/Plataforma-PC-blue)

---

## 📖 Descripción

**Pong Dimension 3D** es un videojuego deportivo, arcade y competitivo en el que dos jugadores se disputan una pelota sobre una mesa de pin-pong en tres dimensiones. La pelota cuenta con física de rebote, distintas velocidades y efectos de iluminación.

Puedes enfrentarte a una **inteligencia artificial** o competir contra otra persona en el mismo dispositivo. La experiencia combina controles fáciles de aprender con una dificultad progresiva, en partidas de **3 a 10 minutos**.

## 📌 Estado del proyecto

Este repositorio documenta el **diseño y planificación** del juego: Game Design Document (GDD), prototipos de baja y alta fidelidad (Figma), aplicación de la metodología **Agile UX** y pruebas con usuarios. El desarrollo en Unity está planteado como prototipo inicial (ver [Alcance del prototipo](#-alcance-del-prototipo)).

## 📋 Ficha técnica

| Característica | Detalle |
|---|---|
| Nombre provisional | Pin Dimension 3D |
| Género | Deportivo, arcade y competitivo |
| Plataforma objetivo | PC (adaptable posteriormente a consolas) |
| Modo principal | 1 jugador contra IA |
| Modo adicional | 2 jugadores en la misma pantalla |
| Perspectiva | Tercera persona / cámara dinámica |
| Motor | Unity 3D |
| Lenguaje | C# |
| Público objetivo | Jugadores casuales e interesados en juegos deportivos sencillos |
| Duración de partida | 3 a 10 minutos |

## 🎯 Objetivo del jugador

- Devolver la pelota con la paleta sin dejar que rebote dos veces en tu propio lado.
- Anotar puntos haciendo que el rival no pueda devolverla.
- Adaptarse a los cambios de velocidad y dirección.
- Ganar la partida al alcanzar la cantidad de puntos establecida (5, 7, 11 o 21).

## 🎮 Modos de juego

- **Partida contra IA:** un jugador humano contra la computadora.
- **Dos jugadores locales:** dos personas en el mismo teclado o con controles conectados.
- **Práctica:** prueba rebotes y velocidades sin marcador.
- **Desafío de velocidad:** la pelota aumenta gradualmente su rapidez.

## 🕹️ Controles

| Acción | Jugador 1 | Jugador 2 (modo local) |
|---|---|---|
| Mover la paleta | `W` `A` `S` `D` | Flechas del teclado |
| Golpe especial / impulso* | `Espacio` | — |
| Pausar | `Esc` | — |

\* Si se implementa. En modo individual, la IA controla automáticamente al segundo jugador.

## ⚙️ Mecánicas principales

### Paletas
- Se desplazan horizontal y verticalmente dentro de los límites de su área.
- No pueden atravesar la mesa ni la red, ni salir de la zona permitida.
- Pueden inclinarse ligeramente para modificar la dirección del rebote.

### Pelota y física
- Usa `Rigidbody` y `Collider` para simular su movimiento.
- Rebota en la mesa, la paleta y, en algunos casos, la red; la dirección depende del punto de contacto.
- Velocidad mínima (para que no quede casi inmóvil) y máxima (para mantener el equilibrio).
- Efecto de giro (*spin*) planteado como mejora futura.

### Velocidades
Lenta (aprendizaje) · Normal (estándar) · Rápida (reflejos) · Progresiva (aumenta tras varios intercambios).

### Puntuación
Se obtiene un punto cuando el rival no logra devolver la pelota; esta se reinicia al centro después de cada punto. Al terminar se muestra una pantalla de victoria, derrota o empate.

## 🎥 Cámara dinámica

Sigue la pelota y ajusta su posición para mantener la acción visible:

- Seguimiento automático de la pelota y movimiento lateral según su posición.
- Zoom ligero cuando la pelota alcanza alta velocidad.
- Cambio suave de ángulo en rebotes importantes.
- Opción de cámara fija o con movimiento reducido para mayor comodidad.
- Nunca debe ocultar la pelota ni generar movimientos bruscos.

## 🤖 Inteligencia artificial

La IA controla la paleta del segundo jugador en el modo individual: detecta la posición de la pelota, calcula un punto aproximado de intercepción y se mueve hacia él, con un pequeño retraso y errores controlados para no ser perfecta. Regresa a una posición defensiva cuando la pelota está lejos.

| Nivel | Reacción | Precisión | Error |
|---|---|---|---|
| Fácil | Lenta | Baja | Frecuente |
| Normal | Media | Media | Moderado |
| Difícil | Rápida | Alta | Poco frecuente |

## 🎨 Arte, iluminación y audio

- **Estilo:** 3D limpio, deportivo y ligeramente futurista; prioriza la claridad visual y la lectura rápida de la pelota.
- **Iluminación:** luz principal, de relleno y de fondo; sombras dinámicas; reflejos ligeros en la mesa; rastro/brillo de la pelota a alta velocidad; postprocesado opcional (bloom, ambient occlusion, corrección de color).
- **Audio:** sonidos de golpe, rebote, red y punto; golpes normales y fuertes diferenciados; música opcional.

## 🧱 Arquitectura del proyecto

| Script | Responsabilidad |
|---|---|
| `GameManager` | Estado general de la partida y marcador |
| `BallController` | Velocidad, dirección y rebotes de la pelota |
| `PaddleController` | Movimiento y límites de cada paleta |
| `AIController` | Movimiento del jugador controlado por la computadora |
| `CameraController` | Seguimiento de la pelota y encuadre |
| `UIManager` | Marcador, menús y mensajes |
| `AudioManager` | Efectos de sonido y música |
| `LightingManager` | Iluminación y efectos visuales |

## 🔁 Flujo de juego

1. El jugador entra al menú principal (Jugar, Opciones, Controles, Salir).
2. Selecciona el modo de juego.
3. Elige dificultad, velocidad y cantidad de puntos.
4. La partida inicia con la pelota en el centro.
5. Los jugadores mueven sus paletas; la pelota rebota según las colisiones.
6. Quien falla da un punto al rival y la pelota se reinicia.
7. Al alcanzar la puntuación objetivo se muestra el resultado.
8. El jugador puede volver a jugar o regresar al menú.

## 🚧 Alcance del prototipo

- [ ] Una mesa funcional
- [ ] Pelota con rebote y límites de velocidad
- [ ] Dos paletas controlables
- [ ] Modo un jugador contra IA
- [ ] Marcador y condición de victoria
- [ ] Cámara dinámica básica
- [ ] Iluminación con sombras
- [ ] Efectos de sonido principales

## 🔮 Mejoras futuras

- Personalización de paletas y pelotas
- Más escenarios y ambientes
- Modo en línea y sistema de ranking
- Golpes con efecto y distintos tipos de *spin*
- Torneos y campeonatos
- Repeticiones de los mejores puntos
- IA con aprendizaje de patrones del jugador
- Compatibilidad con controles y realidad virtual

## 🔬 Diseño UX y pruebas con usuarios

### Problemas detectados

1. **Cámara dinámica difícil de controlar:** puede moverse demasiado rápido o cambiar de ángulo de forma inesperada, haciendo que el jugador pierda de vista la pelota.
2. **IA demasiado difícil:** puede frustrar a jugadores principiantes.
3. **Exceso de velocidad de la pelota:** el jugador puede no tener tiempo de reaccionar.

### Metodología Agile UX

| Sprint | Enfoque | Resultado esperado |
|---|---|---|
| 1 | Investigación y planificación | Problemas y necesidades de los usuarios claros |
| 2 | Diseño de soluciones (cámara, niveles de IA, velocidades) | Propuestas de diseño que mejoren la jugabilidad |
| 3 | Desarrollo del prototipo | Prototipo funcional con las mejoras |
| 4 | Pruebas con usuarios | Detectar qué problemas persisten |
| 5 | Evaluación y mejora | Mejor usabilidad, aprendizaje y diversión |

### Resultados de la encuesta (3 jugadores)

| Métrica | Resultado |
|---|---|
| Experiencia general | 5/5, 4/5 y 4/5 (promedio ≈ 4.3/5) |
| Entendieron el objetivo | Muy fácil / Fácil / Muy fácil |
| Volverían a jugar | 2 Sí, 1 Tal vez |
| Dificultad | 2 la consideraron equilibrada, 1 difícil |
| Velocidad de la pelota | 2 adecuada, 1 demasiado rápida |

**Lo que más gustó:** la sensación de Pong en perspectiva 3D, el diseño de la cancha, la jugabilidad y que las partidas son rápidas.

**Mejoras sugeridas:**
- Un **tutorial** inicial para jugadores nuevos.
- Controles más claros y ajuste de la velocidad de la pelota.
- Más variedad de canchas, modos y niveles de dificultad.
- Efectos de sonido, distintos tipos de pelota y mejor aspecto visual de las paletas.

## ⚠️ Riesgos y soluciones

| Riesgo | Solución propuesta |
|---|---|
| La pelota atraviesa objetos | Usar *Continuous Collision Detection* y ajustar colliders |
| La pelota se queda quieta | Aplicar velocidad mínima y revisar la física |
| La cámara pierde la pelota | Limitar distancia y mantener un encuadre seguro |
| IA demasiado difícil | Agregar retraso, error y límites de reacción |
| Baja visibilidad | Reducir postprocesado y aumentar el contraste |

## ✅ Criterios de éxito

- El jugador entiende los controles en menos de un minuto.
- La pelota rebota de manera consistente y predecible.
- La cámara mantiene la acción visible.
- La IA ofrece una dificultad equilibrada.
- Una partida se completa sin errores importantes.
- Resulta entretenido tanto contra IA como contra otra persona.

## 💻 Requisitos técnicos

- **Motor:** Unity 3D
- **Lenguaje:** C#
- **Física:** Rigidbody, Colliders y Physics Materials
- **Cámara:** Cinemachine o sistema de cámara programado
- **Rendimiento objetivo:** 60 FPS en una computadora de gama media
- **Resolución inicial:** 1920 × 1080, con soporte para otras resoluciones

## 📁 Documentación

- Game Design Document (GDD): `docs/GDD_Pong_Dimension_3D.pdf`
- Prototipos de baja y alta fidelidad: _(agrega aquí el enlace a Figma)_

## 👤 Autor

**Javier Alejandro Argaez Hernández**

---

_Proyecto académico de diseño UX de videojuegos._
