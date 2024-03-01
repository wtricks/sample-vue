<template lang="">
    <table>
        <thead>
            <tr>
                <th>First name</th>
                <th>Last name</th>
                <th>Address</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="customer of props.customers" :key="customer.id">
                <td>{{customer.fname}}</td>
                <td>{{customer.lname}}</td>
                <td>{{customer.address}}</td>
                <td>
                    <button type="button" title="Delete current customer" @click="$emit('delete', customer.id)">Delete</button>
                    <button type="button" title="Update current customer" @click="$emit('edit', customer.id)">Update</button>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script setup lang="ts">
    import type Customer from './Customer';

    // @ts-ignore
    const props = defineProps<{ customers: Customer[] }>();

    defineEmits(['delete', 'edit']);
</script>

<style scoped>
    table {
        margin-top: 2rem;
        border: 1px solid;
        border-collapse: collapse;
        width: 100%;
    }

    table td,
    table th {
        padding: 0.4rem 0.8rem;
        border: 1px solid;
    }

    table td {
        text-align: left;
    }

    table button {
        font-size: 0.8rem;
        margin: 0 0.2rem;
    }

    table tr td:last-child {
        text-align: center;
    }
</style>../Customer