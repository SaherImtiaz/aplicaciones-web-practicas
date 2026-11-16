## A6. Rutas que no funcionan

### Estructura del proyecto

```text
proyecto/
├── index.html
├── contacto.html
├── apuntes.pdf
└── imagenes/
    ├── logo.png
    └── equipo.jpg
```

### 1. Comprobación de las rutas

| N.º | Código original | ¿Funciona? | Explicación |
|:---:|---|:---:|---|
| 1 | `<img src="logo.png" alt="Logo">` | No | La imagen está dentro de la carpeta `imagenes`. |
| 2 | `<img src="imagenes/equipo.jpg" alt="Equipo">` | Sí | La ruta y el nombre del archivo son correctos. |
| 3 | `<a href="Contacto.html">Contacto</a>` | No | El archivo se llama `contacto.html`, con c minúscula. |
| 4 | `<a href="apuntes.pdf">Apuntes</a>` | Sí | El archivo está en la misma carpeta que `index.html`. |
| 5 | `<a href="imagenes/apuntes.pdf">Apuntes</a>` | No | El archivo PDF no está dentro de la carpeta `imagenes`. |
| 6 | `<img src="imagenes/equipo.png" alt="Equipo">` | No | El archivo se llama `equipo.jpg`, no `equipo.png`. |

### 2. Código corregido

```html
<img src="imagenes/logo.png" alt="Logo">

<img src="imagenes/equipo.jpg" alt="Equipo">

<a href="contacto.html">Contacto</a>

<a href="apuntes.pdf">Apuntes</a>

<a href="apuntes.pdf">Apuntes</a>

<img src="imagenes/equipo.jpg" alt="Equipo">
```

### 3. Explicación

Las rutas relativas dependen de la ubicación del archivo desde el que se escriben. En este caso, todas las rutas parten de `index.html`.

También hay que tener cuidado con los nombres de los archivos, las extensiones y las mayúsculas y minúsculas, porque muchos servidores web las diferencian.
