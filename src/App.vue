<template>
  <div id="app">
   
    <div v-if="!logged">
     
      <h1>Sign Up</h1>
      <form id="signup">
        <p>
          <label>Firstname: <input type="text" name="firstname" v-model="user.firstname"> </label>
        </p>
        <p>
          <label>Lastname: <input type="text" name="lastname" v-model="user.lastname"> </label>
        </p>
        <p>
          <label>Email: <input type="email" name="email" v-model="user.email"> </label>
        </p>
        <p>
          <label>Password: <input type="password" name="password" v-model="user.password"> </label>
        </p>
         <button @click.prevent="signup">Create</button>
      </form>
      
      <h1>Sign In</h1>
      <form id="signin">
        <p>
          <label>Email: <input type="email" name="email" v-model="user.email"> </label>
        </p>
        <p>
          <label>Password: <input type="password" name="password" v-model="user.password"> </label>
        </p>
         <button @click.prevent="signin">Sign In</button>
      </form>
      
      <hr />
      
      
      
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      logged: false,
      loading: true,
      questions: [],
      answers: [],
      user: {
        firstname: '',
        lastname: '',
        email: '',
        password: '',
      },
      question: {
        text: '',
        user: '',
        answers: ''
      },
      
    }
  }
}
</script>

<style>

</style>
