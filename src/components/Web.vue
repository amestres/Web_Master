<template>
    <div class="container-main">
        <div class="container-menu" v-if="rol === 'normal'">
            <BotonMenu v-for="opciones in 3" :key="opciones"></BotonMenu>
        </div>
        <div class="container-menu" v-else-if="rol === 'administrador'">
            <BotonMenu v-for="opciones in 2" :key="opciones"></BotonMenu>
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
            
        }
    },
    props:["id","rol"],
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
       background-color: rgb(13, 108, 252);
       color: white;
    }

</style>
