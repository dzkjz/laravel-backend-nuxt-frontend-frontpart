<template>
  <div class="container col-md-6 mt-5">
    <h2>User Dashboard</h2>
    <hr>
    <h3>Create a new topic</h3>
    <form @submit.prevent="create">
      <div class="form-group">
        <label><strong>Topic Title:</strong></label>
        <input type="text" class="form-control" v-model.trim="form.title" autofocus>
        <small class="form-text text-danger" v-if="errors.title">{{errors.title[0]}}</small>
      </div>
      <div class="form-group">
        <label><strong>Topic Body:</strong></label>
        <textarea class="form-control" rows="5" v-model.trim="form.body"></textarea>
        <small class="form-text text-danger" v-if="errors.body">{{errors.body[0]}}</small>
      </div>
      <button type="submit" class="btn btn-primary">Create</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: "dashboard",
    middleware: ['auth',],
    data() {
      return {
        form: {
          title: '',
          body: '',
        }
      }
    },
    methods: {
      async create() {
        try {
          await this.$axios.post('/topics', this.form);
        } catch (e) {
          return;
        }

        this.$router.push('/');
      }
    }
  }
</script>

<style scoped>

</style>
