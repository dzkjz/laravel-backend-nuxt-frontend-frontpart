<template>
  <div class="container col-md-6 mt-5">
    <h2>Register</h2>
    <br>
    <form @submit.prevent="submit">
      <div class="form-group">
        <label>UserName</label>
        <input type="text" class="form-control" placeholder="Enter your Username" v-model.trim="form.name" autofocus>
        <small class="form-text text-danger" v-if="errors.name">{{errors.name[0]}}</small>
      </div>
      <div class="form-group">
        <label>Email address</label>
        <input type="email" class="form-control" placeholder="Enter your email address" v-model.trim="form.email">
        <small class="form-text text-danger" v-if="errors.email">{{errors.email[0]}}</small>
      </div>
      <div class="form-group">
        <label>Password</label>
        <input type="password" class="form-control" placeholder="Enter your password" v-model.trim="form.password">
        <small class="form-text text-danger" v-if="errors.password">{{errors.password[0]}}</small>
      </div>
      <div class="form-group">
        <label>Confirm Password</label>
        <input type="password" class="form-control" placeholder="Confirm your password"
               v-model.trim="form.password_confirmation">
        <small class="form-text text-danger"
               v-if="errors.password_confirmation">{{errors.password_confirmation[0]}}</small>
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
        try {
          await this.$axios.$post('register', this.form);
        } catch (e) {
          return;
        }

        try {
          this.$auth.loginWith('local', {
            data: {
              email: this.form.email,
              password: this.form.password,
            }
          });
        } catch (e) {
          return;
        }

        //redirect
        this.$router.push('/');
      }
    }
  }
</script>

<style scoped>

</style>
