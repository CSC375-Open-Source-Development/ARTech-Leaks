<template>
  <div>
    <Chat :messages="messages"/>
  </div>
</template>

<script>
import chats from '../resources/chats.json'
import Chat from '../components/Chat.vue'

export default {
  name: 'Home',
  components: {
    Chat
  },
  data: () => {
    return {
      messages: []
    }
  },
  mounted() {
    this.messages = chats
  }
}
</script>
