# 🎃🕵️‍♀️ EL IMPOSTOR: Edda’s Edition - Master Plan (iOS PWA - Edición Fiesta de Cumpleaños)

## Contexto & Visión
Aplicación Web Progresiva (PWA) con estética nativa **Apple iOS Human Interface Guidelines (HIG)**:
- **Diseño**: Dark mode nativo de iOS (`#000000` con `#1C1C1E`), glassmorphism con capas de desenfoque (`backdrop-filter: blur(25px)`), tipografía del sistema San Francisco Pro (-apple-system), bordes redondeados orgánicos (`rounded-2xl`, `rounded-3xl`), y microinteracciones táctiles hápticas visuales (`active:scale-95`).
- **Idioma**: Español Latinoamericano festivo, cálido e interactivo (e.g., "Pásale el teléfono a...", "¡Sos el impostor!", "¿Quién engañó a Edda?").
- **Caso de uso**: Fiesta de cumpleaños de Edda en temática Noche de Brujas (Halloween). Diseñado para jugar en grupo con un solo iPhone/móvil que se pasa entre los invitados. Funciona offline tras la carga inicial.

---

## Fases de Desarrollo & Arquitectura

### FASE 1: Banco de Palabras (8 Categorías Pre-cargadas + Personalizadas)
Categorías integradas en el código:

1. **🎃 Halloween y Terror (Predeterminada)**:
   * *Calabaza, Vampiro, Casa Embrujada, Hombre Lobo, Bruja, Fantasma, Esqueleto, Murciélago, Dulce o Truco, Cementerio, Zombi, Marea Negra, Exorcismo, Gato Negro, Polizón, Sombra, Caldero*.
2. **🎂 Cumpleaños de Edda (Edición Especial Fiesta)**:
   * *Torta de Cumpleaños, Velas, Regalos, Piñata, Cotillón, Globos, Brindis, DJ de Fiesta, Karaoke, Pista de Baile, Confeti, Fiesta Sorpresa, Copas de Champaña, Gafas de Fiesta, Mesa Dulce*.
3. **🎤 Farándula y Pop Latino**:
   * *Bad Bunny, Rosalía, Shakira, Karol G, Met Gala, TikTok, Bizarrap, Coachella, Grammy, Peso Pluma, Duki, Anuel, Taylor Swift, Rauw Alejandro, Maluma*.
4. **🎬 Cine y Series**:
   * *Stranger Things, Harry Potter, Juego de Tronos, Avengers, Batman, Titanic, Squid Game, Beetlejuice, El Exorcista, Merlina, Star Wars, Barbie*.
5. **🍕 Comidas y Bebidas**:
   * *Pizza, Tacos, Fernet, Asado, Hamburguesa, Empanadas, Sushi, Tequila, Cerveza, Churros, Mojito, Helado, Arepas, Guacamole*.
6. **✈️ Viajes y Destinos**:
   * *París, Río de Janeiro, Nueva York, Machu Picchu, Cancún, Roma, Tokio, Buenos Aires, Madrid, Barcelona, Cartagena, Londres, Punta Cana*.
7. **⚽ Deportes y Pasiones**:
   * *Fútbol, Mundial, Lionel Messi, Diego Maradona, Baloncesto, Tenis, Estadio Lleno, Árbitro, Golazo, Fórmula 1, Trofeo, Gimnasio, Boxeo*.
8. **🕯️ Mitos y Leyendas**:
   * *La Llorona, El Chupacabras, Triángulo de las Bermudas, Ovni, Monstruo del Lago Ness, Pie Grande, Maldición, Tablero Ouija, Hechizo, Poción Mágica, Pacto Secreto, Espejo Maldito*.
9. **🛠️ Categorías Personalizadas (LocalStorage)**:
   * Modal interactivo para agregar categorías ilimitadas con nombres personalizados (ej. "Anécdotas de Edda", "Chistes de la Oficina").

---

### FASE 2: Pantallas y Flujo del Juego (iOS HIG Components)

1. **Pantalla 1: Configuración (`SetupView`)**
   - **Mesa de sospechosos**: Agregar y quitar jugadores rápidamente, avatares automáticos, límite de 20 jugadores, guardado seguro en `localStorage`.
   - **Segmented Control iOS**: Elección entre 1 impostor (mínimo 3 jugadores) o 2 impostores (mínimo 5 jugadores).
   - **Opciones de asistencia**: Interruptor tipo Switch iOS para dar pista de categoría al impostor.
   - **Grid de categorías**: Tarjetas táctiles oscuras con soporte multiselección y badges de conteo.

2. **Pantalla 2: Pase de Teléfono y Puerta de Seguridad (`PassView`)**
   - Protocolo anti-espías: solo el jugador activo ve su tarjeta.
   - Botón interactivo "Mantén presionado para ver tu carta" con barra de progreso circular / relleno de 650ms.
   - Si se suelta o se mueve el dedo fuera, la tarjeta se oculta y desenfoca al instante.
   - El botón de siguiente jugador solo se desbloquea tras completar la revelación.

3. **Pantalla 3: Revelación de Carta (`CardRevealView`)**
   - **Tripulante**: Muestra la palabra clave con emoji y categoría.
   - **Impostor**: Alerta roja animada con advertencia "¡SOS EL IMPOSTOR!" y pista sutil (si está activa).

4. **Pantalla 4: Ronda de Pistas y Debate (`GameView`)**
   - Orden aleatorio de participación con corona al primer orador (👑 Comienza). Reordenable antes de la primera pista.
   - Transición automática a **Fase de Debate con Temporizador Circular SVG de 60 segundos**.
   - Controles de Pausa, Continuar y Reinicio a 60s con anuncios de accesibilidad `aria-live`.

5. **Pantalla 5: Votación, Última Oportunidad y Victoria (`VoteView`, `GuessView`, `ResultView`)**
   - Votación en grid táctil para seleccionar al sospechoso o sospechosos.
   - **Última oportunidad del Impostor**: Si los descubren, pueden intentar adivinar la palabra clave para robarse la victoria.
   - Celebración con animación de **Confetti** (`canvas-confetti`), desglose de la partida y botón de reinicio inmediato.

---

### FASE 3: Configuración PWA para iOS Safari & Despliegue
- Meta tags `apple-mobile-web-app-capable`, `apple-mobile-web-app-status-bar-style: black-translucent`.
- Íconos táctiles Apple Touch Icon integrados en base64/SVG.
- Responsive design con soporte para notch, Isla Dinámica y barra de inicio de iPhone (`safe-area-inset`).
- Despliegue en Vercel con un solo clic y opción "Agregar a pantalla de inicio" en iOS Safari.
