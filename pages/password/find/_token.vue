<template>
  <div class="container col-md-6 mt-5">
    <h2>Update your password</h2>
    <br>
    <div class="alert alert-primary" v-for="message in messages">
      {{message}}
    </div>
    <form @submit.prevent="submit">
      <div class="form-group">
        <label>Email address</label>
        <input type="email" class="form-control" v-model.trim="form.email"
               placeholder="Enter email">
        <small class="form-text text-danger" v-if="errors.email">{{errors.email[0]}}</small>
      </div>

      <div class="form-group">
        <label>New Password</label>
        <input type="password" class="form-control" v-model.trim="form.password"
               placeholder="Password">
        <small class="form-text text-danger" v-if="errors.password">{{errors.password[0]}}</small>
      </div>
      <button class="btn btn-primary" type="submit">Login with new password</button>
    </form>
    <br>
    <p>Already have an account?
      <nuxt-link to="/login">Login</nuxt-link>
    </p>
  </div>
</template>

<script>
  export default {
    middleware: ['guest'],
    name: "_token",
    data() {
      return {
        form: {
          email: '',
          password: '',
          token: '',
        },
        messages: [],
        foundUserByToken: false,
      }
    },
    methods: {
      async submit() {

        this.messages = [];
        //根据token找用户
        try {
          let response = await this.$axios.$get(`/password/find/${this.form.token}`)
          console.log('Response:', response);
          this.foundUserByToken = true;
          this.messages.push("We found you...just a second!");
        } catch (e) {
          return;
        }

        if (this.foundUserByToken) {
          //前往重置密码
          try {
            let response = await this.$axios.$post('/password/reset', {
              email: this.form.email,
              password: this.form.password,
              token: this.form.token,
            });
            console.log('password reset is done: ', response);
            this.messages.push("Password reset success!.. just a second!");
          } catch (e) {
            return;
          }


          //登录用户

          try {
            await this.$auth.loginWith('local', {
              data: {
                email: this.form.email,
                password: this.form.password,
              }
            })

            this.messages.push("All Done! Redirecting...")

            //

            this.messages = [];
            this.form = {};
            //redirect
            this.$router.push('/topics');
          } catch (e) {
            return;
          }

        }

      }
    },
    mounted() {
      this.form.token = this.$route.params.token;
      console.log(this.form.token);
    }
  }
</script>

<style scoped>

</style>
