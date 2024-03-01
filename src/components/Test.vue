<script setup>
    import { ref } from 'vue'

    const name = ref("")
</script>

<template>
    <input type="text" placeholder="Enter your name" name="fname" v-model="name" />
    <h1>Hello {{name}}</h1>
</template>