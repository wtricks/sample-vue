<script setup>
    import { ref } from 'vue'

    const name = ref("")
</script>

<template>
    <h1>Hello {{name}}</h1>

    <br>
    <input type="text" placeholder="Enter your name" name="fname" v-model="name" />
    <button type="button" title="Clear Name" @click="name = ''">Clear</button>
    <button type="button" title="Clear Name" @click="name = name.toUpperCase()">Make capital</button>
</template>