<template>
  <div class="container">
    <h1 class="heading">Get to know who you are hacking!</h1>
    <div class="company-container">
      <hr>
      <p class="company-name">ARTech</p>
      <img class="logo" :src="require('../resources/artech-logo.png')">
      <p class="company-description">
        ARTech is a gaming company run by controversial CEO Alex Thimineur. 
        The company is well known world-wide for their innovative game products, and has made billions of dollars in revenue.
        You can see some of the company's critically acclaimed products <a href="https://a-r-t.github.io/SER225-Project-Website/">here</a>.
        While the employees that work for ARTech are top-of-the-line, the CEO himself has faced a ton of criticism over accusations of hostile working conditions.
        The court of public opinion has also grown tired of his can-do attitude.
      </p>
      <hr>
    </div>
    <div class="user-container">
      <div class="user" v-for="(user, index) in users" :key="user.id">
        <p class="name">{{ user.firstName }} {{ user.lastName }}</p>
        <p class="role">{{ user.role }}</p>
        <img class="profile-picture" :src="require(`../resources/profile-pictures/${user.profilePicture}`)">
        <p class="bio">{{ user.bio }}</p>
        <hr v-if="index !== users.length - 1">
      </div>
    </div>
  </div>
</template>

<script>
import users from '../resources/users.json'

export default {
  name: 'About',
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

.heading {
  margin-bottom: 3rem;
}

.company-container {
  width: 30rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.company-name {
  font-size: 1.5rem;
  font-weight: 800;
}

.logo {
  border-radius: 2rem;
}

.company-description {
  margin-bottom: 2rem;
}

.user-container {
  margin-top: 2rem;
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
  margin-bottom: .5rem;
}

.role {
  font-style: italic;
  margin: 0px;
  margin-bottom: 1.3rem;
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