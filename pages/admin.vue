<template>
  <div class="container">
    <h1>Dashboard</h1>
    <button @click="logout" class="btn btn-secondary">Logout</button>
    <p>hello {{$auth.$state.user.name}}</p>
    <hr>

        <form>
    <div class="form-group">
    <label for="title">Title</label>
    <input v-model="title" type="text" class="form-control" placeholder="Enter title">
    </div>
    <div class="form-group">
    <label for="body">Body</label>
    <textarea v-model="description" name="body" class="form-control" cols="30" rows="10"></textarea>
    </div>
    <button type="submit" @click="addPost"  class="btn btn-primary">Create a new Post</button>
      </form>

    <hr>
    <h2>All products</h2>
    <hr>
    <div class="row">

      <div v-for="post in products" :key="post._id" class="col-md-4">
        <div class="card text-white bg-primary mb-3" style="max-width: 20rem;">
      <div class="card-body">
      <h4 class="card-title">{{post.title}}</h4>
      <p class="card-text">{{post.description}}</p>
      </div>
      </div>
      </div>



    </div>
  </div>
</template>

<script>
export default {
  async asyncData({$axios}) {
    try {
      let response = await $axios.$get('http://localhost:4000/api/products')

      console.log(response);
      return {
        products: response.products
      }


    } catch (error) {
      console.log(error);
    }
  },
  data() {
    return {
      title: '',
      description: ''
    }
  },
   methods: {
     async addPost() {
       let data = {
         title : this.title,
         description: this.description
       }
       let result = await this.$axios.$post('http://localhost:4000/api/products' , data)

     },
     async logout() {
    await this.$auth.logout()
    this.$router.push('/')
    }
   },
}
</script>

<style>

</style>
