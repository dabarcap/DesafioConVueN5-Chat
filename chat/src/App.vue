<script>
import axios from 'axios';
import ChatBox from './components/ChatBox.vue';

export default {
  name: 'App',
  components: {
    ChatBox
  },
  data() {
    return {
      user1: {},
      user2: {},
      message1: '',
      message2: '',
      color1: '#000000',  // color de texto para el usuario 1
      color2: '#000000',  // color de texto para el usuario 2
      messages: []        // lista de mensajes
    };
  },
  created() {
    // Cargar los datos de los usuarios al cargar la app
    this.loadUsers();
  },
  methods: {
    async loadUsers() {
      try {
        const response = await axios.get('https://randomuser.me/api/');
        this.user1 = response.data.results[0];
        
        const response2 = await axios.get('https://randomuser.me/api/');
        this.user2 = response2.data.results[0];
      } catch (error) {
        console.error('Error al cargar los usuarios', error);
      }
    },
    sendMessage(user) {
      let newMessage = '';
      let color = '';
      let name = '';

      if (user === 'user1') {
        newMessage = this.message1;
        color = this.color1;
        name = `${this.user1.name.first} ${this.user1.name.last}`;
        this.message1 = '';  // Limpiar el campo de texto
      } else if (user === 'user2') {
        newMessage = this.message2;
        color = this.color2;
        name = `${this.user2.name.first} ${this.user2.name.last}`;
        this.message2 = '';  // Limpiar el campo de texto
      }

      if (newMessage) {
        this.messages.push({ name, message: newMessage, color });
      }
    }
  }
};
</script>

<template>
  <div id="app" class="app-container">
    <div class="user-section">
      <!-- Usuario 1 -->
      <div class="user">
        <img :src="user1.picture.large" alt="User 1" class="user-img" />
        <p>{{ user1.name.first }} {{ user1.name.last }}</p>
        <input type="color" v-model="color1" />
        <textarea v-model="message1" placeholder="Escribe un mensaje"></textarea>
        <button @click="sendMessage('user1')">Enviar</button>
      </div>
    </div>

    <!-- Sección del Chat -->
    <chat-box :messages="messages" :user1Name="user1.name.first" :user2Name="user2.name.first" />

    <!-- Usuario 2 -->
    <div class="user-section">
      <div class="user">
        <img :src="user2.picture.large" alt="User 2" class="user-img" />
        <p>{{ user2.name.first }} {{ user2.name.last }}</p>
        <input type="color" v-model="color2" />
        <textarea v-model="message2" placeholder="Escribe un mensaje"></textarea>
        <button @click="sendMessage('user2')">Enviar</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  justify-content: space-between;
  padding: 20px;
}

.user-section {
  width: 40%;
}

.user {
  margin-bottom: 20px;
  text-align: center;
}

.user-img {
  width: 80%;
  height: 80%;
}

textarea {
  width: 80%;
  height: 100px;
  margin-top: 10px;
}

button {
  margin-top: 10px;
}

input[type="color"] {
  margin-top: 10px;
  width: 80%;
}

button {
  padding: 5px 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
  width: 80%;
}

button:hover {
  background-color: #45a049;
}
</style>
