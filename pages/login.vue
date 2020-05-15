<template>
  <div class="container col-md-6 mt-5">
    <h2>Login</h2>
    <br>
    <form @submit.prevent="submit">
      <div class="form-group">
        <label>Email address</label>
        <input type="email" class="form-control" v-model.trim="form.email" autofocus>
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <div class="form-group">
        <label>Password</label>
        <input type="password" class="form-control" v-model.trim="form.password" autofocus>
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <button type="submit" class="btn btn-primary">Login</button>
    </form>
    <br>
    <p>Don't have an account?
      <nuxt-link to="/register">Register</nuxt-link>
    </p>
  </div>
</template>

<script>
  export default {
    name: "login",
    data() {
      return {
        form: {
          email: '',
          password: '',
        }
      }
    },
    methods: {
      async submit() {
        await this.$auth.loginWith('local', {
          data: this.form,
        });
        this.$router.push('/');
      },
    }

  }
</script>

<style scoped>

</style>
