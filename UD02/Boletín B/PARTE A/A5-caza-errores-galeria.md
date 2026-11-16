## A5. Caza los errores de la galería

### 1. Errores encontrados

1. La etiqueta `<html>` no tiene el atributo `lang="es"` para indicar el idioma.
2. La etiqueta `<title>` está mal cerrada. Debe escribirse `</title>`.
3. La primera imagen tiene mal colocada la etiqueta `src`. Debe estar dentro de `<img>`.
4. La etiqueta `<img>` no necesita cierre, porque es una etiqueta vacía.
5. En la segunda imagen, los valores de `width` y `height` están escritos con `=` en lugar de `:`, porque son propiedades CSS.
6. El enlace tiene la dirección `href` sin comillas.
7. El enlace no está cerrado con `</a>`.
8. El documento no tiene una estructura de cierre correcta para el contenido del enlace.

### 2. Código corregido

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="utf-8">
    <title>Mi galería</title>
</head>
<body>

    <h1>Mi viaje de fin de curso</h1>

    <img src="playa.jpg" alt="Playa al atardecer">

    <img src="monte.jpg" alt="Montaña" style="width: 300px; height: 200px;">

    <a href="https://www.wikipedia.org" target="_blank">
        Más información sobre el destino
    </a>

</body>
</html>
```

---

### 3. Explicación

El código original tenía errores en las etiquetas, los atributos y los estilos CSS. Después de corregirlos, las imágenes pueden mostrarse correctamente y el enlace puede abrir la página de Wikipedia en una pestaña nueva.
