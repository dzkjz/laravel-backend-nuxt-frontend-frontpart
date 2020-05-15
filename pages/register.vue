<template>
  <div class="container col-md-6 mt-5">
    <h2>Register</h2>
    <br>
    <form @submit.prevent="submit">
      <div class="form-group">
        <label>UserName</label>
        <input type="text" class="form-control" placeholder="Enter your Username" v-model.trim="form.name" autofocus>
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <div class="form-group">
        <label>Email address</label>
        <input type="email" class="form-control" placeholder="Enter your email address" v-model.trim="form.email">
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <div class="form-group">
        <label>Password</label>
        <input type="password" class="form-control" placeholder="Enter your password" v-model.trim="form.password">
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <div class="form-group">
        <label>Confirm Password</label>
        <input type="password" class="form-control" placeholder="Confirm your password"
               v-model.trim="form.password_confirmation">
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <button type="submit" class="btn btn-primary">Register</button>
    </form>
    <br>
    <p>Already have an account?
      <nuxt-link to="/login">Login</nuxt-link>
    </p>
  </div>
</template>

<script>
  export default {
    name: "register",
    data() {
      return {
        form: {
          name: '',
          email: '',
          password: '',
          password_confirmation: '',
        }
      }
    },
    methods: {
      async submit() {
        await this.$axios.$post('register', this.form);

        this.$auth.loginWith('local', {
          data: {
            email: this.form.email,
            password: this.form.password,
          }
        });

        //redirect
        this.$router.push('/');
      }
    }
  }
</script>

<style scoped>

</style>
