<script setup lang="ts">
  import Card from './components/Card.vue';
  import CardImage from './assets/card.jpg'

// import Counter from './components/Counter.vue';

// import CustomerList from './components/CustomerList.vue';

// import Test from './components/Test.vue';
</script>

<template>
  <!-- <Test /> -->
  <!-- <CustomerList /> -->

  <!-- <Counter /> -->


  <Card />

  <Card>
    <template #header>
       <img 
          :src="CardImage" 
          alt="No Title"
        />
    </template>

    <template #title>
        A beautiful Sunset
    </template>

    <template #body>
      <p>
        Images of an beatiful sunset looks so eye-catching. View other similer images by clicking on below button.
      </p>
    </template>

    <template #footer>
      <button type="button" title="View More">
        View more
      </button>
    </template>
  </Card>
</template>

<style scoped>
    img {
      aspect-ratio: 3 / 2;
      width: 100%;
      border-radius: 5px;
    }

    p {
      padding: 0 0.2rem;
      text-align: left;
      font-size: 0.9rem;
    }

    button {
      font-size: 0.8rem;
    }
</style>