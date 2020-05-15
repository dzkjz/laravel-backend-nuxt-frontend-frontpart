<template>
  <div class="container col-md-6 mt-5">
    <h2>Login</h2>
    <br>
    <form @submit.prevent="submit">
      <div class="form-group">
        <label>Email address</label>
        <input type="email" class="form-control" v-model.trim="form.email" autofocus>
        <small class="form-text text-danger" v-if="errors.email">{{errors.email[0]}}</small>
      </div>
      <div class="form-group">
        <label>Password</label>
        <input type="password" class="form-control" v-model.trim="form.password" autofocus>
        <small class="form-text text-danger" v-if="errors.password">{{errors.password[0]}}</small>
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
    middleware: ['guest',],
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
        try {
          await this.$auth.loginWith('local', {
            data: this.form,
          });
        } catch (e) {
          return;
        }

        //redirect
        this.$router.push({
          path: this.$route.query.redirect || '/profile',
        });
      },
    }

  }
</script>

<style scoped>

</style>
