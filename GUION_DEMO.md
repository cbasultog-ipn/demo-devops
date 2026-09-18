# Guion de la demostración (10 a 15 minutos)

## Antes de la clase

- [ ] Abre estas pestañas en el navegador, en este orden:
  1. El sitio publicado: https://cbasultog-ipn.github.io/demo-devops/
  2. El repositorio: https://github.com/cbasultog-ipn/demo-devops
  3. La pestaña **Actions** del repositorio
- [ ] Inicia sesión en GitHub con anticipación.
- [ ] Haz una ejecución de prueba completa el día anterior (pasos 2 a 5 de abajo) y **deja el sitio en su estado original** ("Versión 1").
- [ ] Toma capturas de pantalla o un video corto del flujo completo como plan B si falla el internet.

## Idea central que quieres transmitir

> Un cambio pasa por revisiones automáticas antes de llegar a los usuarios. Si algo está mal, el sistema lo detiene solo.

Vocabulario que vas a usar, con su significado en lenguaje simple:

| Término | Significado |
|---------|-------------|
| **Commit** | Guardar un cambio con un registro de quién, cuándo y qué cambió. |
| **Pipeline** | La cadena de pasos automáticos que se ejecuta con cada cambio. |
| **CI (Integración Continua)** | Revisar automáticamente cada cambio (etapa Validar). |
| **CD (Entrega/Despliegue Continuo)** | Publicar automáticamente lo que pasó las revisiones (etapa Desplegar). |
| **Despliegue** | Poner una versión a disposición de los usuarios. |

## Desarrollo

### 1. Punto de partida (2 min)

Muestra el sitio publicado. Pregunta al grupo: *"¿Cuánto tardaría hoy en su organización llevar un cambio de texto a producción?"* (las respuestas suelen ser días o semanas).

Señala la "Huella de esta publicación": el commit y la hora.

### 2. Un cambio que sale bien (4 min)

1. En el repositorio, abre `index.html` y pulsa el ícono del **lápiz**.
2. Busca esta línea y cambia el texto:
   ```html
   <p id="mensaje">Versión 1: primera publicación con el pipeline.</p>
   ```
   Por ejemplo: `Versión 2: cambio hecho durante la clase.`
3. Baja y pulsa **Commit changes** → **Commit changes** de nuevo.
4. Ve a la pestaña **Actions**. Abre la ejecución en curso y muestra las tres etapas avanzando: Validar → Construir → Desplegar.
5. Cuando termine, recarga el sitio. Muestra el mensaje nuevo y que **el commit y la hora cambiaron**.

**Qué decir:** "Nadie subió archivos a un servidor ni corrió comandos. Solo guardé un cambio y el sistema hizo el resto."

### 3. Un cambio que sale mal (4 min): el momento clave

1. Edita `index.html` otra vez.
2. Busca `<h1>Hola DevOps</h1>` y cámbialo a `<h1>Hola</h1>`.
3. Haz **Commit changes**.
4. En **Actions**, muestra la ejecución en **rojo**. Entra a la etapa **Validar** y muestra el mensaje de error:
   *"El título principal (h1) debe decir exactamente: Hola DevOps"*
5. Muestra que las etapas **Construir** y **Desplegar** ni siquiera se ejecutaron.
6. Recarga el sitio: **sigue mostrando la versión anterior sin errores**.

**Qué decir:** "El error se detectó en segundos y nunca llegó a los usuarios. Sin pipeline, alguien lo habría descubierto después de publicarlo."

### 4. Corregir y recuperar (2 min)

1. Regresa `<h1>Hola</h1>` a `<h1>Hola DevOps</h1>` y haz commit.
2. Muestra el pipeline en verde otra vez y el sitio actualizado.

### 5. Cierre (2 min)

Muestra el archivo `.github/workflows/pipeline.yml` y explica que **todo el pipeline es ese archivo de texto**: está versionado, se puede revisar y se puede repetir.

Preguntas para el grupo:
- ¿Qué otras revisiones automáticas agregarían? (ortografía, seguridad, pruebas de rendimiento)
- ¿Qué pasaría si se agregara una aprobación humana antes de desplegar?
- ¿Qué procesos manuales de su trabajo podrían automatizarse así?

## Después de la demo: restaurar el estado original

Deja el repositorio listo para el siguiente grupo. Edita `index.html` y vuelve a poner:

```html
<p id="mensaje">Versión 1: primera publicación con el pipeline.</p>
```

## Solución de problemas

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| El pipeline falla en **Configurar GitHub Pages** o **Desplegar** con un error tipo *"Get Pages site failed"* | GitHub Pages no está activado. | **Settings → Pages → Source: GitHub Actions**. Luego en **Actions** abre la ejecución fallida y pulsa **Re-run all jobs**. |
| El pipeline no arranca | El archivo no está en la ruta exacta. | Debe estar en `.github/workflows/pipeline.yml`, con el punto inicial. |
| El sitio muestra `__COMMIT__` o `__FECHA__` | Estás viendo el archivo sin construir o una versión en caché. | Abre la URL de `github.io` y recarga con `Ctrl + F5`. |
| El sitio muestra error 404 | Aún no termina el primer despliegue. | Espera un minuto y revisa que la etapa **Desplegar** esté en verde. |
| Alguien pregunta por qué tarda | Cada etapa inicia una máquina virtual nueva. | Normal: suele tardar de 30 a 90 segundos en total. |

## Ideas para ampliar la demo

- **Aprobación manual:** en **Settings → Environments → github-pages**, activa *Required reviewers* para exigir que una persona autorice cada despliegue.
- **Ejecución manual:** en **Actions → Pipeline de demostración → Run workflow**.
- **Segunda validación:** agrega en `pipeline.yml` un paso más que revise otra condición (por ejemplo, que exista la palabra "pipeline").
