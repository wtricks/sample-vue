<template>
    <form method="post" action="/create" class="input-box" @submit.prevent="onSubmitForm">
        <input id="fname" type="text" placeholder="Enter first name" v-model="fname" />
        <input id="lname" type="text" placeholder="Enter last name" v-model="lname" />
        <input id="address" type="text" placeholder="Enter address" v-model="address" />
        <button type="submit" title="Add into list">
            {{ !props.customer ? "Add" : "Update" }}
        </button>
    </form>
</template>

<script setup lang="ts">
    import { ref, watchEffect } from 'vue';
    import type Customer from './Customer'

    const props = defineProps<{  customer: Customer  }>()

    const emit = defineEmits(['addOrUpdate'])

    const fname = ref('')
    const lname = ref('')
    const address = ref('')

    // we'll update or create a customer based on condition
    const onSubmitForm = () => {
        if (!fname.value || !lname.value || !address.value) {
            return
        }

        const data: Customer = {
            id: Math.random(),
            fname: fname.value,
            lname: lname.value,
            address: address.value
        }

        fname.value = lname.value = address.value = '';
        emit('addOrUpdate', data)
    }

    watchEffect(() => {
        if (props.customer) {
            fname.value = props.customer.fname
            lname.value = props.customer.lname
            address.value = props.customer.address
        }
    })
</script>

<style>
    form {
        width: 100%;
        display: flex;
        justify-items: flex-start;
        margin-top: 2rem;
        border: 1px solid;
        padding: 0.5rem;
    }

    form input {
        margin: 0 0.2rem;
    }

    form button {
        margin-left: auto;
    }
</style>../Customer