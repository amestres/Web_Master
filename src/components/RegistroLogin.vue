<template>
    <div id="formulario-registro">
        <div class="container-botones">
            <button class="boton" id="botonRegistrar" @click="cambiarFormularioRegistro">Registrarme</button>
            <button class="boton" id="botonLogin" @click="cambiarFormularioLogin">Ya tengo cuenta</button>
        </div>
        <div class="container-formularios">
            <form v-if="formulario === 1" onsubmit="event.preventDefault()">
                <div class="container-separador">
                    <label for="login" class="label-formulario">Login</label>
                    <input v-model="formData.login" type="text" name="login" required>
                </div>
                <div class="container-separador">
                    <label for="password" class="label-formulario">Password</label>
                    <input v-model="formData.password" type="password" name="password" required>
                </div>

                <div class="container-separador">
                    <label for="nombre" class="label-formulario">Nombre</label>
                    <input v-model="formData.nombre" type="text" name="nombre" required> 
                </div>
                
                <div class="container-separador">
                    <label for="apellidos" class="label-formulario">Apellidos</label>
                    <input v-model="formData.apellidos" type="text" name="apellidos" required>
                </div>

                <input type="submit" id="boton-submit-registrar" @click="crearUsuario" value="Registrar usuario">
            </form>
            <form v-if="formulario === 2" onsubmit="event.preventDefault()">
                <div class="container-separador">
                    <label for="login" class="label-formulario">Login</label>
                    <input v-model="formData.login" type="text" name="login" required>
                </div>
                
                <div class="container-separador">
                    <label for="password" class="label-formulario">Password</label>
                    <input v-model="formData.password" type="password" name="password" required>
                </div>

                <input type="submit" id="boton-submit-login" @click="verificarFormularioLogin" value="Entrar">
            </form>
        </div>  
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'RegistroLogin',
    data() {
        return{
            formData:{
                login: '',
                password: '',
                nombre: '',
                apellidos: '',
            },
            formulario: 1
        }
    },
    methods:{
        cambiarFormularioRegistro(){
            this.formulario = 1
            this.resetInputs()
        },

        cambiarFormularioLogin(){
            this.formulario = 2
            this.resetInputs()
        },
        resetInputs(){
            this.formData.login = ''
            this.formData.password = ''
            this.formData.nombre = ''
            this.formData.apellidos = ''
        },
        async crearUsuario(){
            const response = await axios.post('http://localhost/api/?servicio=registrar_usuario',{ 
                login : this.formData.login, 
                password : this.formData.password, 
                nombre : this.formData.nombre, 
                apellidos : this.formData.apellidos
            })

            //Mostramos por consola que mensaje nos ha devuelto la api
            if(response.data.data["resultado"] === "ok"){
                console.log("Usuario registrado")
                this.$emit('entrar', response.data.data["id"], "normal")
            }
            else{
                if(response.data.data["resultado"] === "login_usuario_ya_existe"){
                    console.log("Ya existe ese login")
                }
            }
        },
        async verificarFormularioLogin(){
            const response = await axios.post('http://localhost/api/?servicio=login',{
                login : this.formData.login, 
                password : this.formData.password, 
            })

            if(response.data.data["resultado"] === "ok"){  
                console.log("Usuario encontrado")
                this.$emit('entrar', response.data.data["id"], response.data.data["rol"])
            }
            else{
                if(response.data.data["resultado"] === "no_ok"){
                    console.log("Usuario no encontrado")
                }
            }
        }
    }
}
</script>

<style scoped>
    #formulario-registro{
        background-color: white;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .container-botones{
        width: 50%;
        display: flex;
        justify-content: center;
    }

    .boton{
        width: 16rem;
        height: 4rem;
        margin: 2rem;
        border: 0.5px solid black;
        border-radius: 20px;
        font-size: 20px;
        background-color: rgb(13, 108, 252);
        color: white;
    }

    .boton:hover{
        background-color: #3246fc;
        box-shadow: 0 .125rem .25rem rgba(0, 0, 0, .30);
    }

    .boton:visited{
        background-color: #3246fc;
    }

    .container-formularios{
        display: flex;
        justify-content: center;
    }

    .container-separador{
        margin-top: 10px;
        justify-content: center;
        border-radius: .5rem;
        padding: .75rem 1rem .25rem;
        background-color: #E7EFFF;
    }

    input{
        width: 100%;
        background-color: #E7EFFF;
        font-size: var(--normal-font-size);
        border: none;
        outline: none;
        padding: .25rem .5rem .5rem 0;
    }

    .label-formulario{
        font-size: .813rem;
    }

    #boton-submit-registrar, #boton-submit-login{
        width: 16rem;
        height: 4rem;
        margin: 2rem;
        border: 0.5px solid black;
        border-radius: 20px;
        font-size: 20px;
        background-color: rgb(13, 108, 252);
        color: white;
    }

    #boton-submit-registrar:hover, #boton-submit-login:hover{
        background-color: #3246fc;
        box-shadow: 0 .125rem .25rem rgba(0, 0, 0, .30);
    }

</style>
