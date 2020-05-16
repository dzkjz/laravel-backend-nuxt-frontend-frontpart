<template>
  <div class="container">
    <h2>Update Post</h2>
    <form @submit.prevent="update">
      <div class="form-group mt-5">
        <textarea class="form-control" v-model="post.body" rows="5"></textarea>
        <small class="form-text text-danger" v-if="errors.body">{{errors.body[0]}}</small>
      </div>

      <button class="btn btn-outline-success">Update</button>
    </form>
    <p class="mt-5 btn btn-outline-warning">
      <nuxt-link to="/topics">Back to Topics</nuxt-link>
    </p>
  </div>
</template>

<script>
  export default {
    name: "index",
    data() {
      return {
        post: {
          body: '',
        }
      }
    },
    async asyncData({$axios, params}) {
      let {data} = await $axios.$get(`/topics/${params.id}/posts/${params.postid}`);
      return {
        post: data,
      }
    },
    methods: {
      async update() {
        await this.$axios.patch(`/topics/${this.$route.params.id}/posts/${this.$route.params.postid}`,
          {body: this.post.body});
        //redirect
        this.$router.push('/topics');
      },
    }
  }
</script>

<style scoped>

</style>
