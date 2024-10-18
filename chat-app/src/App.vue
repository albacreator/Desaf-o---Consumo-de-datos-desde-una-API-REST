<template>
  <div id="app" v-if="users.length > 0">
    <h1>Chat entre Desconocidos</h1>
    <div class="card-container">
      <div class="user-card">
        <img :src="users[0]?.picture.large" :alt="`${users[0]?.name.first} ${users[0]?.name.last}`" class="user-picture" />
        <h2>{{ users[0]?.name.first }} {{ users[0]?.name.last }}</h2>
        <MessageInputComponent 
          :users="users" 
          @sendMessage="agregarMensaje" 
          :userIndex="0"
        />
      </div>
      <div class="messages-card">
        <ChatComponent :messages="messages" :users="users" />
      </div>
      <div class="user-card">
        <img :src="users[1]?.picture.large" :alt="`${users[1]?.name.first} ${users[1]?.name.last}`" class="user-picture" />
        <h2>{{ users[1]?.name.first }} {{ users[1]?.name.last }}</h2>
        <MessageInputComponent 
          :users="users" 
          @sendMessage="agregarMensaje" 
          :userIndex="1"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ChatComponent from './components/ChatComponent.vue';
import MessageInputComponent from './components/MessageInputComponent.vue';

export default {
  components: {
    ChatComponent,
    MessageInputComponent,
  },
  data() {
    return {
      users: [],
      messages: [],
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get('https://randomuser.me/api/?results=2');
        this.users = response.data.results;
      } catch (error) {
        console.error('Error al cargar los usuarios:', error);
      }
    },
    agregarMensaje(messageContent, userIndex) {
      const newMessage = {
        content: messageContent,
        user: this.users[userIndex].name.first,
        color: userIndex === 0 ? 'lightblue' : 'lightgreen',
      };
      this.messages.push(newMessage);
    },
  },
};
</script>

<style>
.card-container {
  display: flex;
  justify-content: space-around;
  margin: 20px;
}
h1{
  text-align: center;
}
.user-card {
  flex: 1;
  text-align: center;
}

.messages-card {
  flex: 2;
  margin: 0 20px;
}
.user-picture {
  border-radius: 50%;
  width: 80px;
  height: 80px;
}
</style>
