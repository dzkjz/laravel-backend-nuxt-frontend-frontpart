<template>
  <div class="container col-md-6 mt-5">
    <h2>Register</h2>
    <br>
    <form>
      <div class="form-group">
        <label>First Name</label>
        <input type="text" class="form-control" placeholder="Enter your first name">
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <div class="form-group">
        <label>Last Name</label>
        <input type="text" class="form-control" placeholder="Enter your last name">
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <div class="form-group">
        <label>Email address</label>
        <input type="email" class="form-control" placeholder="Enter your email address">
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <div class="form-group">
        <label>Password</label>
        <input type="password" class="form-control" placeholder="Enter your password">
        <small class="form-text text-danger">Show errors here</small>
      </div>
      <div class="form-group">
        <label>Confirm Password</label>
        <input type="password" class="form-control" placeholder="Confirm your password">
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
    name: "register"
  }
</script>

<style scoped>

</style>
