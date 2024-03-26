<template>
  <div class="container">
    <p>Get to know the team that we are hacking!</p>
    <div class="user" v-for="(user, index) in users" :key="user.id">
      <p class="name">{{ user.firstName }} {{ user.lastName }}</p>
      <img class="profile-picture" :src="require(`../resources/profile-pictures/${user.profilePicture}`)">
      <p class="bio">{{ user.bio }}</p>
      <hr v-if="index !== users.length - 1">
    </div>
  </div>
</template>

<script>
import users from '../resources/users.json'

export default {
  name: 'Users',
  data: () => {
    return {
      users: users.sort((a, b) => `${a.firstName} ${a.lastName}`.localeCompare(`${b.firstName} ${b.lastName}`))
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

.user {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 2rem;
}

.name {
  font-size: 1.5rem;
  font-weight: 800;
  margin: 0px;
  margin-bottom: 1.5rem;
}

.profile-picture {
  width: 10rem;
  border-radius: 80px;
}

.bio {
  width: 30rem;
  margin-bottom: 2rem;
}

hr {
  border: 0;
  clear: both;
  display: block;
  width: 96%;               
  background-color:green;
  height: 1px;
}
</style>