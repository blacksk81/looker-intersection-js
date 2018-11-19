<h1>Observador de intersection de imagenes JS</h1>
	<h2>by:luisbernal</h2>

<p>Este pequeño scritp nos ayudara a la carga asincronica de imagenes el campo visual de la pantalla de esta manera las images que estan fuera del campo visual de la pantalla del usuario su carga se encontrara en espera hasta que sea visible para el usuario, pero para que la carga no sea tan grotesta y de golpe agregaremos un pequeño css para que la transcion mas suave entre images</p>


<p>Paso uno Agregar el CSS de la etiqueta img cambiar scr por data-scr</p>

<pre>
	.fade-in {
      animation-name: fadeIn;
      animation-duration: 1.3s;
      animation-timing-function: cubic-bezier(0, 0, 0.4, 1);
      animation-fill-mode: forwards;
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
      }

      to {
        opacity: 1;
      }
    }
</pre>

<p>Paso dos cambio de atributto a nuestra etiqueta SCR</p>

<pre>

 src="cometanike.png
 <br>
 data-src="cometanike.png

</pre>

<p>Paso tres agregar el siguiente scritp a nuestra web al final</p>

<pre>

'use strict';
 var images = document.querySelectorAll('img'),
     config = {
         rootMargin: '50px 0px',
         threshold: 0.01
     },
     imageCount = images.length,
     observer;
 if (!('IntersectionObserver' in window)) loadImagesImmediately(images);
 else {
     observer = new IntersectionObserver(onIntersection, config);
     for (var image, i = 0; i < images.length; i++)(image = images[i], !image.classList.contains('js-lazy-image--handled')) && observer.observe(image)
 }

 function fetchImage(a) {
     return new Promise(function(b, c) {
         var d = new Image;
         d.src = a, d.onload = b, d.onerror = c
     })
 }

 function preloadImage(a) {
     var b = a.dataset.src;
     return b ? fetchImage(b).then(function() {
         applyImage(a, b)
     }) : void 0
 }

 function loadImagesImmediately(a) {
     for (var d, b = Array.from(a), c = 0; c < a.length; c++) d = a[c], preloadImage(d)
 }

 function disconnect() {
     observer && observer.disconnect()
 }

 function onIntersection(a) {
     0 === imageCount && observer.disconnect();
     for (var c, b = 0; b < a.length; b++) c = a[b], 0 < c.intersectionRatio && (imageCount--, observer.unobserve(c.target), preloadImage(c.target))
 }

 function applyImage(a, b) {
     a.classList.add('js-lazy-image--handled'), a.src = b, a.classList.add('fade-in')
 }	

</pre>

<p><b>ESTA FUNCION ESTA SOLO PARA LA CARGA DE IMAGENES</b></p>