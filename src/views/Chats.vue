<template>
  <div class="container">
    <p class="select-conversation-label">Select Conversation</p>
    <div class="listbox">
      <p v-for="(conversation, index) in conversations" :key="conversation.id" @click="onConversationSelected(index)" :id="`conversation-${index}`" class="no-margin unselectable">{{ conversation.id }}</p>
    </div>
    <div class="move-buttons-container">
      <button class="move-button" @click="moveUp">&#9650;</button>
      <button class="move-button" @click="moveDown">&#9660;</button>
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
      conversations: [],
      selectedConversationIndex: 0
    }
  },
  mounted() {
    const conversationIds = require.context('@/resources/conversations', false, /.json$/).keys().map(key => key.slice(2, -5))
    this.conversations = conversationIds.map(conversationId => ({ id: conversationId })).sort((a, b) => parseInt(a.id) - parseInt(b.id))

    this.$nextTick(() => {
      const conversationId = this.$route.query.conversation
      if (!conversationId) {
        return this.onConversationSelected(0)
      }
      const index = this.conversations.findIndex(conversation => conversation.id === conversationId)
      if (index === -1) {
        return this.onConversationSelected(0)
      }
      return this.onConversationSelected(index)
    });
  },
  computed: {
    messages() {
      if (this.conversations[this.selectedConversationIndex]) {
        const conversation = require(`../resources/conversations/${this.conversations[this.selectedConversationIndex].id}.json`)
        return conversation
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
    onConversationSelected(index) {
      const previousConversationSelection = document.getElementById(`conversation-${this.selectedConversationIndex}`)
      previousConversationSelection.style.backgroundColor = 'white';
      previousConversationSelection.style.color = 'black';
      const conversationSelection = document.getElementById(`conversation-${index}`)
      conversationSelection.style.backgroundColor = 'green'
      conversationSelection.style.color = 'white';
      this.selectedConversationIndex = index
      this.$el.querySelector(`#conversation-${index}`).scrollIntoView({ behavior: 'auto', block: 'nearest', inline: 'nearest' })
      return this.$router.replace({ name: 'Chats', query: { conversation: this.conversations[index].id } })
        .catch(() => {})
    },
    moveUp() {
      if (this.selectedConversationIndex > 0) {
        this.onConversationSelected(this.selectedConversationIndex - 1)
      }
    },
    moveDown() {
      if (this.selectedConversationIndex < this.conversations.length - 1) {
        this.onConversationSelected(this.selectedConversationIndex + 1)
      }
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
  width: 30rem;
  color: black;
  cursor: pointer;
  height: 6rem;
  overflow-y: scroll;
  border: 1px solid black;
  margin-bottom: 1rem;
}

.move-buttons-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.move-button {
  width: 5rem;
  height: 1.5rem;
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
