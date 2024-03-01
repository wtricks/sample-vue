<template>
    <h1>Customer Details</h1>

    <Form 
        @add-or-update="onAddOrUpdate" 
        :customer="customers[currentEditIndex]"
    />

    <List 
        :customers="customers" 
        @delete="(id: number) => deleteCustomerDetail(id)" 
        @edit="(id: number) => editCustomerDetail(id)" 
    />
</template>
<script lang="ts" setup>
    import { reactive, ref } from 'vue';
    import Form from './Form.vue'
    import List from './List.vue'
    import type Customer from './Customer';
    
    // hold customers
    const customers = reactive<Customer[]>([]);
    const currentEditIndex = ref(-1); // hold index of item, which is currently updating

    const onAddOrUpdate = (data: Customer) => {
        if (currentEditIndex.value != -1) {
            data.id = customers[currentEditIndex.value].id
            customers[currentEditIndex.value] = data
            currentEditIndex.value = -1
        } else {
            customers.push(data)
        }
    }

    // TODO: We can also use Array index instead of customer "id"
    const editCustomerDetail = (id: number) => {
        const index = customers.findIndex(customer => customer.id == id);
        currentEditIndex.value = index;
    }

    // TODO: We can also use Array index instead of customer "id"
    const deleteCustomerDetail = (id: number) => {
        const index = customers.findIndex(customer => customer.id == id);

        if (currentEditIndex.value == index) {
            alert("Customer is being updating!")
            return
        }

        customers.splice(index, 1)
    }
</script>

<style>
    h1 {
        font-size: 2rem;
        font-weight: 500;
        text-align: left;
        margin-bottom: 1rem;
    }
</style>