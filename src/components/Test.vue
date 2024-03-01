<script setup lang="ts">
    import { onBeforeMount, onBeforeUnmount, onBeforeUpdate, onErrorCaptured, onMounted, onUnmounted, onUpdated, ref } from 'vue'

    const name = ref("")

    onBeforeMount(() => {
        console.log("Before Mount")
    })

    onMounted(() => {
        console.log("Mounted")
    })

    onBeforeUpdate(() => {
        console.log("State is going to update")  
    })

    onUpdated(() => {
        console.log("State is updated!")  
    })

    onBeforeUnmount(() => {
        console.log("Component is going to unmount")  
    })

    onUnmounted(() => {
        console.log("Component is unmounted already!")  
    })

    onErrorCaptured((err) => {
        console.log("Error: ", err)
    })
</script>

<template>
    <h1>Hello {{name}}</h1>

    <br>
    <input type="text" placeholder="Enter your name" name="fname" v-model="name" />
    <button type="button" title="Clear Name" @click="name = ''">Clear</button>
    <button type="button" title="Clear Name" @click="name = name.toUpperCase()">Make capital</button>
</template>