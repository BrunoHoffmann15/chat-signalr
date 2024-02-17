<template>
  <q-page class="q-pa-md column content-center" style="height: 100%;">
    <div class="column" style="width: 100%; max-width: 40%; height: auto;">
      <div>

        <q-chat-message
          v-for="(mess, index) in listMessages"
          v-bind:key="index"
          :name="mess.user"
          :avatar="mess.userPicture"
          :text="mess.content"
          :stamp="mess.time"
          :sent="mess.isMine"
        />
      </div>
      <div class="q-pa-md row justify-center">
        <q-form
          class="row"
          style="width: 100%;"
          @submit="sendMessage">
          <q-input rounded outlined dense class="WAL__field col-grow q-mr-sm" bg-color="white" v-model="message" placeholder="Type a message" v-on:enter="sendMessage"/>
          <q-btn color="secondary" round icon="send" type="submit"/>
        </q-form>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { date } from 'quasar'

const message = ref('');
const listMessages = ref(
  [{
    content: ["Olá, como você está?"],
    isMine: false,
    time: "10/10/2023",
    userPicture: "https://cdn.quasar.dev/img/avatar1.jpg",
    user: "Roberto"
  }, {
    content: ["Estou bem e você?"],
    isMine: true,
    time: "10/10/2023",
    userPicture: "https://cdn.quasar.dev/img/avatar2.jpg",
    user: "Juliana"
    }
  ]
);

const sendMessage = () => {
  if (!message.value) return;

  const currentTime = date.formatDate(new Date(), 'DD/MM/YYYY');

  const messageToSend = {
    content: [message.value],
    isMine: true,
    userPicture: "https://cdn.quasar.dev/img/avatar2.jpg",
    user: "Juliana",
    time: currentTime
  };

  listMessages.value.push(messageToSend);
  message.value = "";
}
</script>
