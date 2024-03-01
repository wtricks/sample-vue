<script setup lang="ts">
    import BaseButton from './BaseButton.vue';

    import { 
        computed,
        onBeforeMount, 
        onBeforeUnmount, 
        onBeforeUpdate, 
        onErrorCaptured, 
        onMounted, 
        onUnmounted, 
        onUpdated, 
        reactive, 
        ref 
    } from 'vue'

    const color = ref("")
    const name = ref("")
    const date = ref(new Date())
    
    // for our todo list
    const currentListItemIndex = ref(-1);
    const listValue = ref("")
    const listArray  = reactive<string[]>([])

    const deleteListItem = (index: number) => {
        listArray.splice(index, 1)
    }

    const editListItem = (index: number) => {
        listValue.value = listArray[index]
        currentListItemIndex.value = index;
    }

    const addToList = () => {
        if (listValue.value == "") {
            return
        }

        if (currentListItemIndex.value == -1) {
            listArray.push(listValue.value)
        } else {
            listArray[currentListItemIndex.value] = listValue.value
            currentListItemIndex.value = -1
        }
        listValue.value = ''
    } 

    // let interval: number;

    // methods for clearing name
    const clearName = () => {
        name.value = ''
    }

    // methods for make "name" alphabets capital.
    const capitilizeName = () => {
        name.value = name.value.toUpperCase();
    }

    // reverse name
    const reverseName = () => {
        name.value = name.value.split("").reverse().join("")
    }


    const showAlert = () => {
        alert("hello")
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
    <h1 :style="{color}">Hello {{name}}</h1>
    <br>
    {{ currentDate }}
    <br>
    <br>

    <label for="colors">Color</label>
    <select id="colors" name="colros" v-model="color">
        <option value="" selected disabled>No color</option>
        <option value="red">Red</option>
        <option value="green">Green</option>
        <option value="yellow">Yellow</option>
        <option value="blue">Blue</option>
    </select>

    <br>
    <br>
    <input type="text" placeholder="Enter your name" name="fname" v-model="name" />
    <br><br>
    <base-button background-color="#e0a800" text-color="white" @click="showAlert" value="Alert" />
    <base-button background-color="#5a6268" text-color="white" @click="clearName" value="Clear" />
    <button type="button" title="Clear Name" @click="capitilizeName">Make capital</button>
    <base-button background-color="#218838" text-color="white" @click="reverseName" value="Reverse" />

    <br><br><br>
    <input type="text" placeholder="Enter anything..." name="list" v-model="listValue" />
    <button type="button" title="Add message into list" @click="addToList">
        {{ currentListItemIndex != -1 ? "Edit" : "Add" }}
    </button>
    <br>

    <ul>
        <li v-for="(item, index) in listArray">
            {{ index }} - {{ item }}
            <button type="button" title="Delete" @click="deleteListItem(index)">Delete</button>
            <button type="button" title="Delete" @click="editListItem(index)">Edit</button>
        </li>
    </ul>
</template>

<style>
    .red {
        color: red;
    }

    .green {
        color: green;
    }

    ul {
        padding: 0
    }

    li {
        padding: 1rem;
        list-style: none;
        font-size: 1.5rem;
    }

    li button {
        margin-left: 0.8rem;
        font-size: 0.8rem;
    }
</style>