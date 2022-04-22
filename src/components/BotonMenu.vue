<template>
    <div class="container-boton">
        <p>{{texto}}</p>
    </div>
</template>

<script>
export default {
    name: 'BotonMenu',
    data() {
        return{
            
        }
    },
    props:["texto"],
    methods:{
        
    }
}
</script>

<style scoped>
    .container-boton{
        width: 200PX;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: #5271ff;
        color: white;
        border: 1px solid white;
        
    }
</style>
