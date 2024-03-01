<template>
    <button 
        @click="$emit('click')"
        type="button" 
        :style="{ 
            backgroundColor: props.backgroundColor,
            color: props.textColor
        }">
        {{ props.value }}
    </button>
</template>

<script setup lang="ts">
    const props = defineProps<{
        value: string,
        backgroundColor: string,
        textColor: string
    }>()

    defineEmits(['click'])
</script>