# Demo DevOps

Repositorio de demostración para explicar un pipeline de integración y entrega continua (CI/CD) sin necesidad de programar.

La "aplicación" es una página web de un solo archivo (`index.html`). Lo importante es el pipeline que la valida, la construye y la publica automáticamente.

## Cómo funciona

Cada vez que se guarda un cambio (commit) en la rama `main`, GitHub Actions ejecuta tres etapas en orden:

| Etapa | Qué hace | Qué pasa si falla |
|-------|----------|-------------------|
| **1. Validar** | Revisa que `index.html` exista, que el título principal diga `Hola DevOps` y que la página esté completa. | El pipeline se detiene y nada se publica. |
| **2. Construir** | Copia la página a una carpeta de publicación y le agrega el commit y la fecha. | No se publica. |
| **3. Desplegar** | Publica el resultado en GitHub Pages. | El sitio anterior sigue en línea. |

## Estructura

```
demo-devops/
├── index.html                    La página (la "aplicación")
├── .github/workflows/pipeline.yml  El pipeline (las tres etapas)
├── GUION_DEMO.md                 Guion para presentar en clase
└── README.md                     Este archivo
```

## Ver el resultado

- **Sitio publicado:** https://cbasultog-ipn.github.io/demo-devops/
- **Ejecuciones del pipeline:** pestaña **Actions** de este repositorio.

## Probarlo tú mismo

1. Abre `index.html` en GitHub y pulsa el ícono del lápiz para editarlo.
2. Cambia la frase de "Qué trae esta versión" y pulsa **Commit changes**.
3. Ve a **Actions** y observa cómo el pipeline se ejecuta solo.
4. Recarga el sitio publicado: verás tu cambio y un commit y una hora nuevos en la "Huella de esta publicación".
