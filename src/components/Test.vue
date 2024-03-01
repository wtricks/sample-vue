<script setup lang="ts">
    import { 
        computed,
        onBeforeMount, 
        onBeforeUnmount, 
        onBeforeUpdate, 
        onErrorCaptured, 
        onMounted, 
        onUnmounted, 
        onUpdated, 
        ref 
    } from 'vue'

    const isChecked = ref(false)
    const name = ref("")
    const date = ref(new Date())

    // let interval: number;

    // methods for clearing name
    const clearName = () => {
        name.value = ''
    }

    // methods for make "name" alphabets capital.
    const capitilizeName = () => {
        name.value = name.value.toUpperCase();
    }


    // computed properties
    const currentDate = computed(() => {
        return `${date.value.getFullYear()} - ${("0"+date.value.getMonth()).slice(-2)} - ${("0"+date.value.getDate()).slice(-2)}`
    })

    onBeforeMount(() => {
        console.log("Before Mount")
    })

    onMounted(() => {
        console.log("Mounted")

        // interval = setInterval(() => {
        //     date.value = new Date()
        // }, 1000)
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
        
        // clearing interval before destroying this component
        // clearInterval(interval)
    })

    onErrorCaptured((err) => {
        console.log("Error: ", err)
    })
</script>

<template>
    <h1 :class="{red: isChecked, green: !isChecked}">Hello {{name}}</h1>
    <br>
    {{ currentDate }}
    <br>
    <br>

    <input id="check" type="checkbox" name="checkbox" v-model="isChecked" />
    <label for="check">Should be Red</label>

    <br>
    <br>
    <input type="text" placeholder="Enter your name" name="fname" v-model="name" />
    <br><br>
    <button type="button" title="Clear Name" @click="clearName">Clear</button>
    <button type="button" title="Clear Name" @click="capitilizeName">Make capital</button>
</template>

<style>
    .red {
        color: red;
    }

    .green {
        color: green;
    }
</style>