<template>
  <div class="container">
    <h2>Latest Topics</h2>
    <div v-for="(topic,index) in topics" :key="index" class="bg-light mt-5 mb-5" style="padding: 20px">
      <nuxt-link :to="{name:'topics-id',params:{id:topic.id}}">{{topic.title}}</nuxt-link>
      <p class="text-muted">{{topic.created_at}} by {{topic.user.name}}</p>
      <div v-for="(content,index) in topic.posts" :key="index" class="ml-5 content">
        {{content.body}}
        <p class="text-muted">{{content.created_at}} by {{content.user.name}}</p>
      </div>
    </div>
    <nav>
      <ul class="pagination justify-content-center">
        <li v-for="(key,value) in links" class="page-item">
          <a @click.prevent="loadMore(key)" class="page-link">{{value}}</a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
  export default {
    name: "index.vue",
    data() {
      return {
        topics: [],
        links: [],
      }
    },
    async asyncData({$axios}) {
      let {data, links,} = await $axios.$get('/topics');
      return {
        topics: data,
        links,
      }
    },
    methods: {
      async loadMore(key) {
        if (key === null) {
          return;
        }
        let {data, links} = await this.$axios.$get(key);
        return this.topics = {...this.topics, ...data};
      }
    }
  }
</script>

<style scoped>
  .content {
    border-left: 10px solid white;
    padding: 0 10px 0 10px;
  }
</style>
