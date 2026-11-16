## A7. ¿Qué verá el usuario?

### Código HTML

```html
<h2>Mi mascota</h2>

<img src="gato.jpg" alt="Gato durmiendo" style="float: right;">

<p>Se llama Miau y duerme catorce horas al día. Cuando está despierto, intenta apagar el router.</p>

<a href="https://www.w3.org/" target="_blank">
    <img src="logo.png" alt="W3C">
</a>
```

### Respuestas

**a) ¿Dónde aparece la imagen del gato respecto al texto?**

La imagen del gato aparece flotando a la derecha del texto, porque tiene la propiedad CSS `float: right;`.

**b) Si gato.jpg no existe, ¿qué se mostrará?**

Se mostrará el texto alternativo "Gato durmiendo", porque está escrito en el atributo `alt` de la imagen.

**c) ¿Qué ocurre al hacer clic en el logo?**

Se abrirá la página web del W3C en una pestaña nueva, porque el logo está dentro de un enlace y tiene el atributo `target="_blank"`.
