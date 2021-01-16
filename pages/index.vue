<template>
  <div class="container mt-5 contain-login">
    <form class="form-signin mt-5">
      <h1 class="h3 mb-3 font-weight-normal">Please sign in</h1>
      <label for="username" class="sr-only">Username</label>
      <input v-model="email" type="email" class="form-control" placeholder="username" required autofocus>
      <label for="inputPassword" class="sr-only">Password</label>
      <input v-model="password" type="password" class="form-control" placeholder="Password" required>
      <a class="btn btn-lg btn-primary btn-block" @click="onLogin">Sign in</a>
      <p class="mt-5 mb-3 text-muted">&copy; 2017-2018</p>

    </form>
     <button @click="logout">log out</button>
  </div>
</template>

<script>
export default {
  middleware: "auth",
  auth: "guest",

  data() {
   return {
      email: '',
      password: ''
    }
  },
   methods: {
     async onLogin() {
        // let data = {
        //   email : this.email,
        //   password: this.description
        // }
        // let result = await this.$axios.$post('http://localhost:4000/api/auth/login' , data)

        // console.log(result);
  try {

       let response = await this.$auth.loginWith("local" , {
        data: {
          email: this.email,
          password: this.password
        }
      })
      this.$router.push('/admin')


  } catch (error) {
    console.log(error);
  }


   },
   async logout() {
    await this.$auth.logout()
   }
},}
</script>

<style>

</style>
