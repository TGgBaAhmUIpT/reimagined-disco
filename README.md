# reimagined-disco · Timer de rutina

Temporizador de entrenamiento para el móvil. Cada archivo `.html` es una app
completa y autónoma: sin dependencias, sin servidor y sin datos que salgan del
navegador. Se abre y funciona.

**`index.html` es siempre la rutina del mes en curso** (ahora, **noviembre de
2026**). Los meses anteriores se archivan con su nombre (ver [Archivo](#archivo)).

## Cómo usarlo

1. Abre la página publicada (GitHub Pages, rama `main`, raíz) en el navegador
   del móvil. Mejor aún: **«Añadir a pantalla de inicio»** para usarla como app.
2. En la pantalla de inicio, revisa lo que viene preseleccionado:
   - **Semana del plan**: se elige sola por la fecha de hoy.
   - **Sesión de hoy** (A / B): la propone el calendario del mes. Si te saltaste
     una sesión, elige la que tocaba, no la del calendario.
   - **Versión de hoy**: la completa o la reducida, para los días sin tiempo.
   - **Interruptores**: siempre arrancan apagados. Actívalos solo si hoy se
     cumple su condición, que está escrita debajo de cada uno.
3. Elige el **modo de avance** (automático, solo en los cambios de ejercicio o
   confirmando cada fase) y pulsa **▶ Empezar sesión**.

Durante la sesión, el timer narra cada fase: calentamiento articulación por
articulación, cada serie con su **metrónomo de tempo** (pitido grave al bajar,
agudo al subir y seco en las pausas), los descansos con qué hacer en ellos y una
cuenta atrás «colócate» antes de cada ejercicio.

| Control | Qué hace |
|---|---|
| ▶ / ⏸ | Empieza o pausa |
| ⏭ | Salta a la fase siguiente. En las series al máximo, se pulsa al fallar |
| ⏮ | Vuelve a la fase anterior |
| Espacio / ← → | Lo mismo con teclado |
| 🔇 | Silencia el audio |

### Que no se apague la pantalla

La app usa Wake Lock, un vídeo mudo en bucle y un re-anclado al tocar la
pantalla. **Nada de eso funciona dentro de un visor embebido** (la vista previa
de una app de chat o de un gestor de archivos, por ejemplo). Ábrela siempre en
el navegador real del móvil, desde la URL `https://` de GitHub Pages o desde el
icono de la pantalla de inicio.

## Noviembre 2026: un solo timer, tres formatos

La semana elegida decide qué sesión sale:

| Semana | Fechas | Formato | Duración |
|---|---|---|---|
| 1-2 | 2-15 nov | **Hotel**: menos series, A/B y versión reducida | ~20 min |
| 3-4 | 16-29 nov | **Casa**: pierna a 3 series, A/B y versión reducida | ~30 min |
| 5 | 30 nov | **Test Day**: series al máximo técnico, sin A/B ni versión reducida | ~21 min |

- **Interruptores del mes** (semanas 1-4): «Dormí mal» quita la pausa arriba en
  la tracción; «Hoy sin barra» cambia la tracción a fila australiana bajo una
  mesa.
- **Test Day**: el metrónomo cubre hasta un techo de repeticiones. Cuando la
  serie termina, pulsa ⏭ y pasas al descanso, donde se recuerda apuntar el
  resultado. Si el test se aplaza, elige la **Semana 4** y la **Sesión B**.

## Archivo

| Archivo | Rutina |
|---|---|
| [`index.html`](index.html) | **Noviembre 2026** (actual) |
| [`timer-rutina-octubre-2026.html`](timer-rutina-octubre-2026.html) | Octubre 2026 |
| [`timer-rutina-septiembre-2026.html`](timer-rutina-septiembre-2026.html) | Septiembre 2026 |
| [`timer-rutina-agosto-2026.html`](timer-rutina-agosto-2026.html) | Agosto 2026 |
| [`timer-rutina-julio.html`](timer-rutina-julio.html) | Julio 2026 |
| [`timer-rutina-junio.html`](timer-rutina-junio.html) | Junio 2026 |
| [`timer-rutina.html`](timer-rutina.html) | Agosto 2026 (versión anterior, sin nombre de mes) |

## Cambio de mes

1. **Archiva** el `index.html` actual renombrándolo a
   `timer-rutina-<mes>-<año>.html`, con el mes en minúsculas y en español
   (p. ej. `timer-rutina-noviembre-2026.html`). Usa `git mv` para conservar el
   historial.
2. **Sube** el timer nuevo como `index.html`.
3. **Actualiza este README**: el mes actual, su sección propia y la tabla del
   archivo.

```bash
git mv index.html timer-rutina-noviembre-2026.html
cp /ruta/al/timer-2026-12.html index.html
git add -A && git commit -m "Diciembre 2026: nuevo index.html; archiva noviembre"
```

## Cómo se generan

Los timers no se editan a mano. Salen de un motor (plantilla HTML + script de
montaje) y de una ficha JSON por mes con las fases, los tempos y los textos.
Ese motor vive fuera de este repo. Antes de publicar cada timer, el script
comprueba que ninguna serie termine a mitad de repetición, que no se vea ninguna
etiqueta HTML en pantalla y que el JavaScript sea válido, y una prueba en
navegador sin pantalla recorre todas las combinaciones de semana, versión,
sesión e interruptores.

Desde noviembre de 2026, el motor admite **formatos distintos por semana en un
mismo timer**: cada fase indica en qué semanas existe.
