<template>
  <div>
    <Chat :messages="messages" :users="users"/>
  </div>
</template>

<script>
import chats from '../resources/chats.json'
import users from '../resources/users.json'
import Chat from '../components/Chat.vue'

export default {
  name: 'Home',
  components: {
    Chat
  },
  data: () => {
    return {
      messages: [],
      users: {}
    }
  },
  mounted() {
    this.messages = chats
    this.users = this.messages.reduce((acc, curr) => {
      const user = users.find(user => user.id === curr.from)
      return { ...acc, [user.id]: user }
    }, {})
  }
}
</script>
