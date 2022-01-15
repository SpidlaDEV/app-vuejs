<template>
    <!-- Definimos el contenedor de entrada -->
    <div class="input-wrapper">
        <!-- Nos proporciona un mensaje de error-->
        <div class="label">
            <label :for="name">{{ name }}</label>
            <div class="error">{{ error }}</div>
        </div>
        <!-- Contenedor de objetos -->
        <input :id="name" :type="type" :value="value" @input="input" />
    </div>
</template>

<script>
    export default {
        name: 'MyInput',
        // Datos a pasar: Nombre, Reglas, Valor, Tipo de Valor
        props: {
            name:{
                type: String,
                required: true
            },
            rules:{
                type: Object
            },
            value: {
                type: String
            },
            type: {
                type: String
            }
        },
        // Unidad Computada: Usa un método para validar los errores
        computed: {
            error(){  
                return this.validar(this.value);     
            }
        },
        // Unidad de Métodos
        methods: {
            // Valida que se cumpla con las reglas y el tamaño de la cadena de caracteres sea el correcto
            validar(value){
                if (this.rules.required && !value){
                    return 'Requerido';
                }
                if(this.rules.min && value.length < this.rules.min){
                    return `Debe ingresar mínimo ${this.rules.min}`;
                }
            },
            // Obtiene el Valor, Nombre y Estado de Validación del objeto
            input($evt){
                this.$emit('update', {
                    value: $evt.target.value,
                    name: this.name,
                    valid: this.validar($evt.target.value) ? false : true
                });
            }
        }
    }
</script>

<style scoped>
.input-wrapper{
    display: flex;
    flex-direction: column;
}

.error{
    color: red;
}

.label{
    display: flex;    
    justify-content: space-between;
}

input {
    background: none;
    color: black;
    border: 1px solid silver;
    border-radius: 5px;
    padding: 10px;
    font-size: 16px;
    margin: 5px 0;    
}
</style>