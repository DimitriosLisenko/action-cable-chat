<script setup>
import { ref } from 'vue';

const message = ref("");
const messages = ref(['test message1', 'test message2']);

const addNewMessage = () => {
  console.log(message.value);
}
</script>

<template>
  <form class="" @submit.prevent="addNewMessage">
    <div class="">
      <span class="">New Message</span>
    </div>
    <input
        type="text"
        class=""
        placeholder="Awesome message"
        minlength="1"
        maxlength="50"
        v-model.trim="message" />
  </form>
  <div class="">
    <ul class="">
      <li v-for="message in messages">{{ message }}</li>
    </ul>
  </div>
</template>

<style scoped>

</style>
