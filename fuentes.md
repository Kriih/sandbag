# Fuentes de Ilustraciones e Iconos Minimalistas (Sin IA)

Referencia de recursos gratuitos (principalmente **SVG**) para ilustrar ejercicios e interfaces de fitness sin gastar tokens ni límites de generación con IA.

> **Contexto del proyecto:** Se creó esta guía para mantener consistencia visual en [index.html](./index.html) sin depender de generación de imágenes con IA. Actualmente el proyecto usa ilustraciones descargadas en local en `./assets/svg/`.

---

## 1. Específicas de ejercicios (estilo consistente)

| Fuente | Contenido | Formato | Licencia | Notas |
| --- | --- | --- | --- | --- |
| [AlexMollard/Open-Exercise-Art](https://github.com/AlexMollard/Open-Exercise-Art) *(en uso actual)* | 562 ilustraciones de ejercicios (`catalogue.json` + carpeta `svg/`) | SVG y PNG | CC BY-SA 4.0 | Contornos vectoriales minimalistas pensados para UI de apps de fitness. Todos los SVGs usan `fill="currentColor"`. |
| [bryllim/workout-guide](https://github.com/bryllim/workout-guide) | 302 ejercicios (~906 frames) | SVG minimalista de línea (512×512 transparente) | CC BY-SA 4.0 (assets) / MIT (código) | Incluye hasta 3 frames por ejercicio para mostrar el movimiento. También disponible como paquete npm (`@bryllim/workout-guide`). |
| [yuhonas/free-exercise-db](https://github.com/yuhonas/free-exercise-db) | +800 ejercicios con metadatos JSON | Imágenes paso a paso (JPG) | Unlicense (dominio público) | No es dibujo minimalista (es foto), pero es 100% libre y muy completo como base de datos. |

**Comentarios de criterio:**
- **Por qué elegimos `Open-Exercise-Art` para la tier list actual:** tiene la mejor combinación de catálogo amplio (562 ejercicios) y estilo minimalista homogéneo en un solo trazo monocromático (`currentColor`). Eso evita que cada cuadrado de la tier list parezca sacado de un estilo distinto.
- **Cuándo preferir `bryllim/workout-guide`:** si más adelante quieres que al pasar el mouse o abrir el panel lateral el ejercicio muestre una **animación paso a paso** (alternando sus 3 frames SVG).
- **Cuándo preferir `free-exercise-db`:** si alguna vez necesitas una versión **100% dominio público** (sin obligación de atribución CC BY-SA) o quieres importar cientos de ejercicios con músculos primarios/secundarios ya estructurados en JSON.

---

## 2. Ilustraciones e iconos minimalistas generales

| Fuente | Enfoque | Formato | Licencia | Notas |
| --- | --- | --- | --- | --- |
| [SVG Repo](https://www.svgrepo.com/) | Iconos e ilustraciones minimalistas | SVG | Variada (muchos CC0 / MIT) | Sin registro. Conviene buscar en inglés (`squat`, `deadlift`, `dumbbell`, `gym`, `pull up`). |
| [Storyset](https://storyset.com/) | Ilustraciones minimalistas con categoría *fitness* | SVG / PNG | Gratis con atribución | Permite elegir color de acento y animar capas antes de descargar. |
| [unDraw](https://undraw.co/) | Ilustraciones vectoriales minimalistas | SVG / PNG | Open-source (sin atribución obligatoria) | Ideal para portadas, encabezados o estados vacíos; color personalizable. |
| [Iconify](https://icon-sets.iconify.design/) | Packs de iconos de línea (Lucide, Tabler, Phosphor, etc.) | SVG | Open-source (MIT / Apache / ISC según pack) | Muy útil para iconos uniformes de equipamiento, filtros y controles de UI. |
| [The Noun Project](https://thenounproject.com/) | Pictogramas y siluetas por ejercicio exacto | SVG / PNG | Gratis con atribución | Enorme variedad de ejercicios específicos en estilo pictograma minimalista. |

**Comentarios de criterio:**
- Estas páginas sirven mejor como **complemento** que como fuente principal de los 31 ejercicios: `Iconify` es excelente para botones/filtros/categorías; `unDraw` o `Storyset` para banners o pantallas vacías; `SVG Repo` y `The Noun Project` para rellenar algún ejercicio muy raro que no exista en `Open-Exercise-Art`.

---

## 3. Cómo está implementado actualmente (para no perder el contexto)

1. **Enfoque actual de [index.html](./index.html):**
   - Entrenamiento **funcional desde casa / exterior, sin máquinas de gimnasio** (pesa rusa, sacos de arena de 25–50 kg, rack para dominadas/fondos, anillas colgadas en árbol y peso corporal).
   - Evaluado con **6 métricas**: *Fuerza práctica*, *Salud y resistencia*, *Eficiencia de tiempo*, *Seguridad*, *Accesibilidad* y *Diversión*.
   - **Filtros triples con toggle independiente** para ocultar o mostrar **Equipamiento**, **Patrón funcional** y **Músculos** (multi-etiqueta por ejercicio) según convenga.
2. **Assets locales en `./assets/svg/` (35 archivos):**
   - **25 SVGs** descargados de *Open Exercise Art* (`kettlebell-swing`, `pull-up`, `dip`, `ring-row`, `ring-dip`, `ring-support-hold`, `bulgarian-split-squat`, `goblet-squat`, `dead-hang`, `one-arm-dumbbell-shoulder-press`, `skin-the-cat`, `kettlebell-romanian-deadlift`, `dumbbell-lunge`, `l-sit`, `hanging-leg-raise`, `bear-crawl`, `push-up`, `pike-push-up`, `lateral-raise`, `plank`, `burpee`, `jumping-jack`, `crunch`, `torso-twist-stretch`, `bosu-ball-push-up`).
   - **10 SVGs minimalistas propios** (hechos a mano en el mismo estilo monocromático `currentColor` porque *Open Exercise Art* no incluía sacos de arena ni ejercicios específicos en anillas/kettlebell): `sandbag-shoulder.svg`, `sandbag-carry.svg`, `sandbag-squat.svg`, `ring-pushup.svg`, `ring-curl.svg`, `ring-face-pull.svg`, `farmers-walk.svg`, `overhead-carry.svg`, `kb-halo.svg` y `turkish-getup.svg`.
   - Todo se guarda en local para funcionar **100% offline** y cargar al instante.
3. **Por qué usamos `<img>` + filtro CSS en lugar de `fetch()`:**
   - Al abrir un HTML directamente desde el disco (`file://`), el navegador bloquea peticiones `fetch()` locales por CORS, mientras que `<img src="assets/svg/...">` funciona siempre sin levantar servidor.
   - Como los SVGs usan `currentColor`, dentro de un `<img>` siempre se dibujan en negro puro. Para adaptarse a ambos temas, [index.html](./index.html) aplica `--svg-filter` (`invert(0.92)` en modo oscuro e `invert(0.08)` en modo claro) solo a los SVGs locales y al icono de respaldo (`FALLBACK_SVG`). Si agregas una foto/PNG externa a color, el filtro no se aplica.
4. **Mapeos aproximados a tener en cuenta:**
   - `kb-clean-press.svg` ← usa `one-arm-dumbbell-shoulder-press.svg` (postura idéntica de press vertical a un brazo).
   - `standing-twists.svg` ← usa `torso-twist-stretch.svg`.
   - `bosu-squat.svg` ← usa `bosu-ball-push-up.svg` (único ejercicio con Bosu en el catálogo).
5. **Cómo añadir o cambiar imágenes en el futuro:**
   - **Sin tocar código:** usa el botón **+ Añadir ejercicio** en [index.html](./index.html) y pega una ruta relativa (ej. `assets/svg/mi-ejercicio.svg`) o una URL. Si lo dejas vacío, usa un icono minimalista de pesa rusa por defecto.
   - **Desde el catálogo de Open Exercise Art:** basta descargar el `.svg` desde `https://raw.githubusercontent.com/AlexMollard/Open-Exercise-Art/main/svg/<id>.svg` y guardarlo en `./assets/svg/`.
6. **Licencia y atribución:**
   - Como *Open Exercise Art* está bajo **CC BY-SA 4.0**, ya se incluyó el pie de página con créditos y enlace al repositorio original dentro de [index.html](./index.html). Si publicas o redistribuyes el proyecto, mantén esa atribución.
