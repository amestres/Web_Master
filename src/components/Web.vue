<template>
    <div class="container-main">
        <!-- Si el usuario logeado tiene rol normal se muestra un menú -->
        <div class="container-menu" v-if="rol === 'normal'">  
            <img src="../assets/CLUVER.png" alt="logo">
            <BotonMenu v-for="apartado in apartadosNormal" :key="apartado" :texto="apartado"></BotonMenu> 
        </div>

        <!-- Si el usuario logeado tiene rol admin se muestra el menú de administrador -->
        <div class="container-menu" v-else-if="rol === 'administrador'">
            <img src="../assets/CLUVER.png" alt="logo">
            <BotonMenu v-for="apartado in apartadosAdministrador" :key="apartado" :texto="apartado"></BotonMenu>
        </div>
    </div>
</template>

<script>
import BotonMenu from './BotonMenu.vue'

export default {
    name: 'WebLogeado',
    components: {
        BotonMenu
    },
    data() {
        return{
            apartadosNormal : {
                0 : "Inicio",
                1 : "Reservas",
                2 : "Perfil"
            },
            apartadosAdministrador : {
                0 : "Inicio",
                1 : "Crear Comunidad",
                2 : "Usuarios",
            },
        }
    },
    props:["id","rol"],  //Recibimos variables (props) del componente padre (App.vue)
    methods:{
        
    }
}
</script>

<style scoped>
    .container-main{
        width: 100%;
        height: 100%;
    }
    .container-menu{
       width: 100%;
       height: 4rem; 
       display: flex;
       justify-content: center;
       background-color: #5271ff;
       color: white;
    }

</style>
