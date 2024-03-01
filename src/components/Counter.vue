<template>
    <div class="counter__container">
        <h1>{{  counter }}</h1>

        <Control 
            @reset="onReset"
            @start="onStart"
            @stop="onStop"
        />
    </div>
</template>

<script lang="ts" setup>
    import { onUnmounted, ref } from 'vue';
    import Control from './Control.vue';

    const counter = ref(0)

    let interval: number;
    const onStart = () => {
        interval = setInterval(() => {
            counter.value++;
        }, 1000)
    }

    const onStop = () => {
        clearInterval(interval)
    }

    const onReset = () => {
        counter.value = 0;
    }

    onUnmounted(() => {
        // clear interval before destroying counter component
        clearInterval(interval)
    })
</script>

<style>
    h1 {
        text-align: center;
        margin-bottom: 3rem;
        font-size: 8rem;
    }
</style>