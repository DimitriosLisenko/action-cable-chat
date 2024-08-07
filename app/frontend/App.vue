<script setup>
import { ref } from 'vue';
const message = ref("");
const messages = ref([]);
import { createConsumer } from '@rails/actioncable';

const protocol = window.location.protocol === 'https:' ? 'wss' : 'ws';
const consumer = createConsumer(`${protocol}://${window.location.host}/cable`);
const channel = consumer.subscriptions.create({ channel: 'ChatChannel' }, {
  received(data) {
    messages.value.push(data['message']);
  }
});

const addNewMessage = () => {
  channel.perform('speak', { message: message.value });
}
</script>

<template>
  <div id="app">
    <h2>Action Cable Example</h2>
    <div class="info">Type something in the box below and hit enter</div>
    <form @submit.prevent="addNewMessage">
      <input
          type="text"
          placeholder="say something"
          minlength="1"
          maxlength="50"
          v-model.trim="message" />
    </form>
    <div class="messages">
      <ul class="message">
        <li v-for="message in messages">{{ message }}</li>
      </ul>
    </div>
  </div>
</template>
