<template>
    <div>
        <form @submit.prevent="register">
          <label for="name">
            Name:
          </label>
          <input v-model="name" type="text" name="name" value>
          <label for="email">
            Email:
          </label>
          <input v-model="email" type="email" name="email" value>
          <label for="password">
            Password:
          </label>
          <input v-model="password" type="password" name value>
          <button type="submit" name="button">
            Register
          </button>
          <ul v-for="(error, errorKey) in errors" :key="errorKey">
            <li>{{ error }}</li>
          </ul>
          <router-link to="/login">
            Already have an account? Login.
          </router-link>
        </form>
    </div>
</template>
<script>
export default {
  data () {
    return {
      name: '',
      email: '',
      password: '',
      errors: []
    }
  },
  methods: {
    async register () {
      await this.$store
        .dispatch('register', {
          name: this.name,
          email: this.email,
          password: this.password
        })
        .then(() => this.$router.push('/dashboard'))
        .catch( err => {
          this.errors = err.response.data.errors
        })
    }
  }
}
</script>
<style>
</style>
