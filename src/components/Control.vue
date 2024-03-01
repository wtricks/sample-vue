<template>
    <div class="counter_controls">
        <button type="button" title="Start timer" @click="$emit('start')">
            Start
        </button>

        <button type="button" title="Stop timer" @click="$emit('reset')">
            Reset
        </button>

        <button type="button" title="Stop timer" @click="$emit('stop')">
            Stop
        </button>
    </div>
</template>

<script lang="ts" setup>
    defineEmits(['start', 'stop', 'reset'])
</script>

<style>
    .counter_controls {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .counter_controls button {
        margin: 0 0.6rem;
    }
</style>