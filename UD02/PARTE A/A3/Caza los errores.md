### A3. Caza los errores

El código original tiene varios errores en su estructura HTML. Estos son los errores que he encontrado:

**Errores encontrados:**

1. Falta la declaración `<!DOCTYPE html>` al principio del documento.
2. La etiqueta `<title>` no tiene su correspondiente cierre `</title>`.
3. El encabezado `<h1>` se cierra incorrectamente con `</h2>`. Debe cerrarse con `</h1>`.
4. La etiqueta `<b>` está mal cerrada, porque se cierra después de la etiqueta `</p>`.
5. Las etiquetas `<b>` y `<p>` están mal anidadas. Primero debe cerrarse `<b>` y después `<p>`.

**Código HTML corregido:**

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <title>Mi tienda de gadgets</title>
</head>
<body>
    <h1>Ofertas de otoño</h1>
    <p>Auriculares con <b>cancelación de ruido</b></p>
</body>
</html>
```

**Conclusión:**

Después de corregir los errores, el documento HTML tiene una estructura correcta. Todas las etiquetas están bien abiertas y cerradas.
