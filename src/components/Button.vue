<template>
    <!-- Botón personalizado -->
    <button :style="{color, background, disabled}" :disabled="disabled">Botón</button>
</template>

<script>
export default {
    name: 'mybutton',
    // Datos a pasar: Color, Color de Fondo, Desactivado
    props: {
        color: {
            type: String
        },
        background: {
            type: String
        },
        disabled: {
            type: Boolean
        }
    }
}
</script>

<style scoped>
button {
    background: none;
    color: black;
    border: none;
    border-radius: 5px;
    padding: 10px 40px;
    font-size: 16px;
    cursor: pointer;
}
button:hover {
    filter: brightness(125%);
}
button:disabled {
    opacity: 0.5;
}
</style>