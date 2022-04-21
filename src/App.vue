<template>
  <div id="app">
      <RegistroLogin v-if="idUsuario === ''" @entrar="entrarWeb" ></RegistroLogin> <!--entrarWeb se lanza cuando el componente "RegistroLogin" devuelve un $emit con el nombre 'entrar -->
      <WebLogeado v-if="idUsuario != ''" :id="idUsuario" :rol="rolUsuario"></WebLogeado>  <!-- Enviamos al componente "WebLogeado" el id del usuario logeado y el rol que tiene -->
  </div>
</template>

<script>
import RegistroLogin from './components/RegistroLogin.vue'
import WebLogeado from './components/Web.vue'

export default {
  name: 'App',
  components: {
    RegistroLogin,
    WebLogeado
  },
  data() {
    return{
        idUsuario : '',    //Estas 2 variables recibiran valor cuando el usuario se registre o se haga login (method entrarWeb)
        rolUsuario : '',
    }
  },
  methods:{
    entrarWeb(id, rol){   //Esta funcion se lanza con @entrar
      this.idUsuario = id   //Guardamos el valor de los dos parámetros que recibimos
      this.rolUsuario = rol
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  height: 100vh;
}

:root{
  --color-base: 252; /*252 azul*/

  --color-principal: rgb(13, 108, var(--color-base));
  --color-principal-hover: rgb(50, 70, var(--color-base));
  --color-formulario: #E7EFFF;
  --white: white;
}




/* RESET DE LOS ESTILOS DEFAULT */
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}

</style>
