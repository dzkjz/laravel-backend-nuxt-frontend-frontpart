<template>
  <div class="container">
    <div class="bg-light mt-5 mb-5" style="padding: 20px;">
      <h2>{{topic.title}}</h2>
      <p class="text-muted">{{topic.created_at}} by {{topic.user.name}}</p>
      <div v-for="(content,index) in topic.posts" :key="index" class="ml-5 content">
        <p>{{content.body}}</p>
        <div v-if="authenticated">
          <div v-if="user.id===content.user.id">
            <nuxt-link :to="{name:'topics-id-posts-postid-edit',params:{id:topic.id,postid:content.id}}">
              <button class="btn btn-outline-success fa fa-edit pull-right">Edit</button>
            </nuxt-link>
            <button class="btn btn-outline-danger fa fa-trash pull-right"
                    @click.prevent="deletePost(content.id)">
              Delete
            </button>
          </div>
        </div>
        <p class="text-muted">{{content.created_at}} by {{content.user.name}}</p>

      </div>
    </div>
    <div class="mt-5 ml-5 mb-5" v-if="authenticated">
      <form @submit.prevent="create">
        <div class="form-group">
          <h4>Add a new Post</h4>
          <textarea class="form-control" placeholder="Write Something" v-model="body" autofocus rows="5"></textarea>
          <small class="form-text text-danger" v-if="errors.body">{{errors.body[0]}}</small>
        </div>
        <button class="btn btn-outline-success">Add Post</button>
      </form>
    </div>
  </div>
</template>

<script>
  export default {
    name: "index.vue",
    data() {
      return {
        topic: '',
        body: '',
      }
    },
    async asyncData({$axios, params}) {
      const {data} = await $axios.$get(`/topics/${params.id}`);
      return {
        topic: data,
      }
    },
    methods: {
      async create() {
        await this.$axios.post(`/topics/${this.$route.params.id}/posts`,
          {
            body: this.body,
          });
        //redirect
        this.$router.push(`/topics`);
      },
      async deletePost(postId) {
        await this.$axios.delete(`/topics/${this.$route.params.id}/posts/${postId}`);
        //redirect
        this.$router.push('/topics');
      },
    }
  }
</script>

<style scoped>

</style>
