#  BREAK | Pausas Activas
 
Aplicación web para docentes y estudiantes del nivel secundario que propone **pausas activas** listas para hacer en el aula: actividades de baile, movimiento, canto, palabras, juegos mentales y dinámicas grupales.
 
Cada actividad ya viene armada, con el sonido, el ritmo o las palabras elegidos, los pasos numerados, la duración y los materiales. No necesita instalación, cuenta ni conexión a un servidor: funciona con HTML, CSS y JavaScript puros.
 
<img width="806" height="839" alt="image" src="https://github.com/user-attachments/assets/7cacabee-6541-4e88-9e56-d5374bdd793b" />

##  Funciones
 
- **Ruleta de categorías:** el azar elige el tipo de pausa.
- **Asistente BREAK:** escribís (o decís con el micrófono) qué necesitás y la app elige una actividad. Si escribís "sentados", prioriza las que se hacen en el lugar.
- **Lista por categoría:** al tocar una categoría se abre una ventana con todas sus pausas activas, con su duración.
- **Mis rutinas:** cada docente puede crear sus propias pausas activas (nombre, categoría, duración y descripción) y verlas en una lista aparte.
- **Música para la pausa:** menú con 6 canciones para reproducir mientras se realiza la actividad, con pausa y botón de detener.
- **Lectura en voz alta:** el botón "Escuchar" lee la actividad completa.
- **Sin repeticiones:** la app recuerda las actividades que ya mostró para no repetirlas seguido.
- **Diseño adaptable:** se ve bien en computadora, tablet y celular.
## Estructura del proyecto
 
```
pausa_activa/
├── index.html          # Estructura, actividades y lógica (JavaScript)
├── css/
│   └── estilos.css     # Estilos y diseño
└── audio/
    ├── cancion.mp3
    ├── cancion1.mp3
    ├── cancion2.mp3
    ├── cancion3.mp3
    ├── cancion4.mp3
    └── cancion5.mp3
```
<img width="828" height="210" alt="image" src="https://github.com/user-attachments/assets/54a23a95-9f07-47f5-a1ae-3ab1ff276f4c" />

##  Cómo funciona por dentro
Todo el código de la aplicación está en la etiqueta `<script>` de `index.html`, organizado en secciones numeradas.
<img width="835" height="703" alt="image" src="https://github.com/user-attachments/assets/e1a50104-8422-40dc-ab2b-045e002228f5" />
### Flujo para generar una actividad
 
```
Ruleta / Asistente / Lista de categoría
              │
              ▼
   Se determina la categoría
              │
              ▼
   actividadSinRepetir(categoria)
              │  consulta el historial (localStorage)
              ▼
   crearActividad(categoria, descripcion, duracion)
              │  elige una actividad al azar
              │  (filtra las "sentado" si se pidió)
              ▼
   mostrarActividad(actividad)
              │
              ▼
   Pantalla: título, duración, recuadro destacado,
             pasos, materiales y botones
```

 
##  Cómo usarla
### Desde la web
 
Entrá a [https://TU-PROYECTO.vercel.app](https://TU-PROYECTO.vercel.app) desde cualquier navegador, en computadora o celular. No hace falta instalar nada. Como el sitio usa HTTPS, el micrófono y la música funcionan sin problemas.
 
### En tu computadora (para modificarla)
 
1. Clonás el repositorio:
```bash
git clone https://github.com/TU-USUARIO/pausa_activa.git
```
2. Abrís la carpeta `pausa_activa`.
3. Hacés doble clic en `index.html`.
> **Recomendado:** abrirla con la extensión **Live Server** de VS Code (clic derecho sobre `index.html` → *Open with Live Server*). Así el navegador no bloquea el micrófono ni la música.
 
## Cómo funciona
 
Todo el contenido está dentro de `index.html`, en la etiqueta `<script>`:
 
| Elemento | Qué contiene |
|---|---|
| `categorias` y `emojis` | Las 6 categorías y su ícono |
| `actividades` | Las 36 actividades base (6 por categoría) |
| `cierres` | Frases de cierre que se agregan al azar |
 
Cada actividad tiene este formato:
 
```js
{
  titulo: "Ronda de sonidos",
  duracion: "3 minutos",
  destacado: " Sonidos: \"tsss\", \"pum-pum\", \"ta-ka-ta-ka\", \"uuuh\"",
  pasos: [
    "Primer paso...",
    "Segundo paso..."
  ],
  materiales: "No necesita materiales.",
  sentado: true   // opcional: se puede hacer sin levantarse
}
```
 
### Agregar una actividad al código
 
1. Abrí `index.html` y buscá la lista de la categoría (por ejemplo `"Canto": [`).
2. Copiá un bloque de actividad, pegalo a continuación y cambiá sus datos.
3. Guardá y recargá la página.
### Agregar o cambiar canciones
 
1. Copiá el archivo `.mp3` dentro de la carpeta `audio/`.
2. En `index.html`, dentro de `<div id="menuCanciones">`, agregá un botón nuevo:
```html
<button type="button" class="song-option" data-src="audio/mi-cancion.mp3">
  ▶️ 7. Mi canción
</button>
```
 
>  **Derechos de autor:** subí a un repositorio público solo música que sea tuya, libre de derechos o con licencia que lo permita (por ejemplo, Creative Commons). Si usás canciones comerciales, es mejor mantener el repositorio privado.
 
## Dónde se guardan los datos
 
La aplicación **no usa servidor ni base de datos**. Guarda la información en el navegador (`localStorage`):
 
| Clave | Qué guarda |
|---|---|
| `break_historial` | Actividades ya mostradas, para no repetirlas |
| `break_total` | Cantidad de pausas generadas |
| `break_mis_rutinas` | Las pausas creadas por el usuario |
 
Esto significa que **las rutinas creadas solo existen en ese dispositivo y ese navegador**. Si se borran los datos del navegador, se pierden, y no se comparten con otros docentes.
 
##  Compatibilidad
 
| Función | Navegadores |
|---|---|
| Ruleta, listas, rutinas y música | Todos los navegadores actuales |
| Lectura en voz alta | Chrome, Edge, Safari, Firefox |
| Reconocimiento de voz (micrófono) | Chrome y Edge (requiere HTTPS o Live Server) |
 
##  Tecnologías
 
- HTML5
- CSS3 (variables, grid, flexbox, animaciones)
- JavaScript (sin librerías ni frameworks)
- Web Speech API (voz) y `localStorage`
- Fuente [Poppins](https://fonts.google.com/specimen/Poppins) de Google Fonts
##  Ideas para seguir mejorando
 
- Convertirla en **PWA** instalable y con funcionamiento sin conexión.
- Exportar e importar rutinas en un archivo `.json` para compartirlas entre docentes.
- Banco compartido de actividades con inicio de sesión (Firebase o Supabase) y aprobación de un administrador.
- Temporizador con cuenta regresiva para cada actividad.
## 📄 Licencia
 
Elegí la licencia que prefieras para tu proyecto (por ejemplo, [MIT](https://choosealicense.com/licenses/mit/)) y agregá el archivo `LICENSE` al repositorio.
 

