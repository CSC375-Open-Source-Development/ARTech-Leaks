<template>
  <div>
    <Chat :messages="messages" :users="users"/>
  </div>
</template>

<script>
import chats from '../resources/chats.json'
import users from '../resources/users.json'
import Chat from '../components/conversation/Conversation.vue'

export default {
  name: 'Home',
  components: {
    Chat
  },
  computed: {
    messages() {
      return chats
    },
    users() {
      return this.messages.reduce((acc, curr) => {
        if (acc.find(user => user.id === curr.from)) {
          return acc
        }
        const user = users.find(user => user.id === curr.from)
        return [ ...acc, user ]
      }, [])
    }
  }
}
</script>
