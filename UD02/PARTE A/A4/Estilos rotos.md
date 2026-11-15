### A4. Estilos rotos

El código original tiene errores en los estilos CSS y en algunas etiquetas HTML. A continuación, explico los errores y escribo cómo se deben corregir.

**1. Primera línea:**

Código original:
```html
<h1 style="color:red font-size:40px;">Directo esta noche</h1>
```

**Error:** Falta un punto y coma (`;`) después de `red`, que sirve para separar las propiedades CSS.

Código corregido:
```html
<h1 style="color:red; font-size:40px;">Directo esta noche</h1>
```

**2. Segunda línea:**

Código original:
```html
<p style="text-align=center;">Estreno de temporada</p>
```

**Error:** Se utiliza el signo igual (`=`) en lugar de los dos puntos (`:`) para indicar el valor de la propiedad CSS.

Código corregido:
```html
<p style="text-align:center;">Estreno de temporada</p>
```

**3. Tercera línea:**

Código original:
```html
<p style="background-color:yellow;">Sorteo de una tarjeta gráfica<p>
```

**Error:** La etiqueta `<p>` del final está mal escrita porque se vuelve a abrir el párrafo en lugar de cerrarlo. Debe utilizarse `</p>`.

Código corregido:
```html
<p style="background-color:yellow;">Sorteo de una tarjeta gráfica</p>
```

**Conclusión:**

Los errores estaban en la sintaxis de CSS y en el cierre de una etiqueta HTML. Después de corregirlos, los estilos se aplican correctamente y el código tiene una estructura adecuada.
