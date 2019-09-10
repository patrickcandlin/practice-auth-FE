<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <form>
      <label>Username</label>
      <input type='text' v-model="username" />
      <label>Password</label>
      <input tupe='text' v-model="password" />
    </form>
    <button @click="sendFetch">click me to send fetch</button>
    <button @click="sendLogin">log-in</button>
    <button @click="getJwt">lets get this JWT Yo</button>
  </div>
</template>

<script>


export default {
  name: 'app',
  data(){
    return {
      username: "",
      password: ""
    }
  },
  methods: {
    sendFetch() {
      fetch('http://localhost:3000/api/v1/users', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Accept: 'application/json'
        },
        body: JSON.stringify({
          user: {
              username: this.username,
              password: this.password,
              bio: 'King of Flavortown',
          }
        })
      })
        .then(r => r.json())
        .then(console.log)
    },
    sendLogin(){
       fetch('http://localhost:3000/api/v1/login', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Accept: 'application/json'
        },
        body: JSON.stringify({
          user: {
              username: this.username,
              password: this.password,
          }
        })
      })
        .then(r => r.json())
        .then(response =>{
          console.log(response)
          localStorage.setItem('jwt', response.jwt)
        })
    },
    getJwt(){
      console.log()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
