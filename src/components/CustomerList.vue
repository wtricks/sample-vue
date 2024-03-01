<template>
    <h1>Customer Details</h1>
    <form method="post" action="/create" class="input-box" @submit.prevent="onSubmitForm">
        <input id="fname" type="text" placeholder="Enter first name" v-model="fname" />
        <input id="lname" type="text" placeholder="Enter last name" v-model="lname" />
        <input id="address" type="text" placeholder="Enter address" v-model="address" />
        <button type="submit" title="Add into list">
            {{ currentEditIndex == -1 ? "Add" : "Update" }}
        </button>
    </form>

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
            <tr v-for="customer of customers">
                <td>{{customer.fname}}</td>
                <td>{{customer.lname}}</td>
                <td>{{customer.address}}</td>
                <td>
                    <button type="button" title="Delete current customer" @click="deleteCustomerDetail(customer.id)">Delete</button>
                    <button type="button" title="Update current customer" @click="editCustomerDetail(customer.id)">Update</button>
                </td>
            </tr>
        </tbody>
    </table>
</template>
<script lang="ts" setup>
    import { reactive, ref } from 'vue';

    interface Customer {
        fname: string,
        lname: string,
        address: string,
        id: number
    }

    // hold customers
    const customers = reactive<Customer[]>([]);
    const currentEditIndex = ref(-1); // hold index of item, which is currently updating
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

        if (currentEditIndex.value == -1) {
            customers.push(data)
        } else {
            data.id = customers[currentEditIndex.value].id // we don't need to use new "id"
            customers[currentEditIndex.value] = data
            currentEditIndex.value = -1;
        }

        fname.value = lname.value = address.value = '';
    }

    // TODO: We can also use Array index instead of customer "id"
    const editCustomerDetail = (id: number) => {
        const index = customers.findIndex(customer => customer.id == id);
        currentEditIndex.value = index;

        const { fname: fv, lname: lv, address: av } = customers[index];

        // added inputs values
        fname.value = fv;
        lname.value = lv;
        address.value = av;
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
</style>