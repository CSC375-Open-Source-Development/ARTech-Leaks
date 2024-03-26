<template>
  <div class="container">
    <p class="select-conversation-label">Select Conversation</p>
    <div class="listbox">
      <p v-for="(chat, index) in chats" :key="chat.id" @click="onChatSelected(index)" :id="`chat-${index}`" class="no-margin unselectable">{{ chat.id }}</p>
    </div>
    <hr>
    <Conversation :messages="messages" :users="users"/>
  </div>
</template>

<script>
import users from '../resources/users.json'
import Conversation from '../components/conversation/Conversation.vue'

export default {
  name: 'Home',
  components: {
    Conversation
  },
  data: () => {
    return {
      chats: [],
      selectedChatIndex: 0
    }
  },
  mounted() {
    const conversationIds = require.context('@/resources/conversations', false, /.json$/).keys().map(key => key.slice(2, -5))
    this.chats = conversationIds.map(conversationId => ({ id: conversationId }))

    this.$nextTick(() => {
      const conversationId = this.$route.query.conversation
      if (!conversationId) {
        return this.onChatSelected(0)
      }
      const index = this.chats.findIndex(chat => chat.id === conversationId)
      if (index === -1) {
        return this.onChatSelected(0)
      }
      return this.onChatSelected(index)
    });
  },
  computed: {
    messages() {
      if (this.chats[this.selectedChatIndex]) {
        const chat = require(`../resources/conversations/${this.chats[this.selectedChatIndex].id}.json`)
        return chat
      }
      return []
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
  },
  methods: {
    onChatSelected(index) {
      const previousChatSelection = document.getElementById(`chat-${this.selectedChatIndex}`)
      previousChatSelection.style.backgroundColor = 'white';
      previousChatSelection.style.color = 'black';
      const chatSelection = document.getElementById(`chat-${index}`)
      chatSelection.style.backgroundColor = 'green'
      chatSelection.style.color = 'white';
      this.selectedChatIndex = index
      return this.$router.replace({ name: 'Chats', query: { conversation: this.chats[index].id } })
        .catch(() => {})
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.select-conversation-label {
  margin: 0px;
  margin-bottom: 1rem;
  margin-top: 2rem;
}

.listbox {
  margin-bottom: 2rem;
  width: 30rem;
  color: black;
  cursor: pointer;
  height: 6rem;
  overflow-y: scroll;
  border: 1px solid black;
}

select option  {
  background-color: green;
  color: white;

}

hr {
  border: 0;
  clear: both;
  display: block;
  width: 40%;               
  background-color:green;
  height: 1px;
}

.unselectable {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.no-margin {
  margin: 0;
}
</style>
