<template>
  <div class="card col-md-5 login-form mt-3">
    <img src="https://image.freepik.com/free-vector/cute-shopping-cart-logo_23-2148453859.jpg" class="card-img-top" alt="Cart Logo" height="200px" width="1500px">
    <div class="card-body p-0">
      <div class="input-group mb-3 mb-0">
        <div class="input-group-prepend">
          <span class="input-group-text" id="basic-addon3">Email</span>
        </div>
        <input type="email" class="form-control" aria-describedby="basic-addon3" v-model="email" placeholder="Enter your email" required>
      </div>
      <div class="input-group mb-3 mb-0">
        <div class="input-group-prepend">
          <span class="input-group-text" id="basic-addon3">Password</span>
        </div>
        <input type="password" class="form-control" aria-describedby="basic-addon3" v-model="password" placeholder="Enter your password" required>
      </div>
    </div>
    <button type="button" class="btn btn-primary col-3 p-1 mb-2 btn-login" @click.prevent="login">Login</button>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    login () {
      const obj = {
        email: this.email,
        password: this.password
      }
      this.$store.dispatch('login', obj)
        .then(response => {
          console.log('masuk sinii >>>>', response)
          localStorage.setItem('access_token', response.data.access_token)
          this.$router.push('/home')
        })
        .catch(error => {
          this.$alert(error.response.data.message)
        })
        .finally(() => {
          this.email = ''
          this.password = ''
        })
    }
  }
}
</script>

<style>

</style>
