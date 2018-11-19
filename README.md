<h1>Observador de intersection de imagenes JS</h1>
	<h2>by:luisbernal</h2>

<p>Este pequeño scritp nos ayudara a la carga asincronica de imagenes el campo visual de la pantalla de esta manera las images que estan fuera del campo visual de la pantalla del usuario su carga se encontrara en espera hasta que sea visible para el usuario, pero para que la carga no sea tan grotesta y de golpe agregaremos un pequeño css para que la transcion mas suave entre images</p>


<p>Paso uno Agregar el CSS</p>

<code>
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
</code>

<p>Paso dos cambio de atributto a nuestra etiqueta SCR</p>

<code>
	
DE  <img  width="400" height="400" src="cielo.jpg"> <br> a <br>   <img  width="400" height="400" data-src="cielo.jpg">

</code>