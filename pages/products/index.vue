<template>
  <div class="container">
      <h1>Create a post</h1>
      <form>
    <div class="form-group">
    <label for="title">Title</label>
    <input v-model="title" type="text" class="form-control" placeholder="Enter title">
    </div>
  <div class="form-group">
    <label for="body">Body</label>
    <textarea v-model="description" name="body" class="form-control" cols="30" rows="10"></textarea>
  </div>
  <a @click="addPost()" class="btn btn-primary">Submit</a>
</form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: null,
      description: null
    }
  },
  methods: {
    async addPost() {
      let data = {
        title: this.title,
        description: this.description
      }

      let result = await this.$axios.$post('http://localhost:4000/api/products' , data)

      this.$router.push('/')
    }
  },
}
</script>
