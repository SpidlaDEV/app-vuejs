<template>
<!-- Título de la página -->
  <my-password />
  <!-- Formulario del Inicio de Sesión -->
  <form @submit.prevent="enviar" class="form">
    <!-- Primer Input: Ingreso del nombre de Usuario -->
    <my-input 
      name="Usuario"
      :rules="{ required: true, min:5 }"
      :value="usuario.value"
      @update="update"
      type="text"
    />
    <!-- Segundo Input: Ingreso de la contraseña del usuario -->
    <my-input
      name="Password"
      :rules="{ required: true, min:10 }"
      :value="password.value"
      @update="update"
      type="password"
    />
    <!-- Botón de logueo -->
    <my-button
      color="white"
      background="darkslateblue"
      :disabled="!valid"
    /> 
  </form>
</template>

<script>
// Exportación de los componentes
import MyPassword from './components/Password.vue'
import MyButton from './components/Button.vue'
import MyInput from './components/MyInput.vue'

export default {
  name: 'App',
  components: {
    MyPassword,
    MyButton,
    MyInput
  },
  data(){
    return {      
      usuario: {
        value: '',
        valid: false
      },
      password:{
        value: '',
        valid: false
      } 
    }
  },
  // Unidad Computada: Usa un método para detectar si el usuario cumplio con las reglas
  computed: {
    valid(){
      return this.usuario.valid && this.password.valid
    }
  },
  // Unidad de Métodos
  methods:{
    // Indica que se ha logueado correctamente
    enviar(){      
      console.log('Enviar');
    },
    // Actualización del componente
    update(payload){      
      this[payload.name.toLowerCase()] = {
      value: payload.value,
      valid: payload.valid
    };
  }
  }
}
</script>

<style>
body{
  font-family: arial;
}

.form{
  max-width: 400px;
  width: 50%;
}
</style>
