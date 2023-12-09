<script setup>

import { ref } from 'vue'
const champ = ref('')

</script>

<template>

    
	<input v-model="champ" placeholder="ingresa tu nombre" />

        <p>Message is: {{ champ }}</p>

        <button @click="increment">search {{ count }}</button>

</template>

<style>
    p{
        color:white
    }
    input::placeholder{
        text-align: center;
    }
    button{
        margin-top:1rem;
    }

</style>