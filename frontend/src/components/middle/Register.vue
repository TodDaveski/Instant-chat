<template>
  <div id="Register">
    <h1>
      Register
    </h1>
    <form method="post" @submit.prevent="onRegister">
      <label for="username">Login:</label>
      <input name="login" type="text" v-model="login"/>
      <label for="password">Password: </label>
      <input name="password" type="text" v-model="password">
      <input type="submit">
      <div class="error">
        {{error}}
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Register",
  methods: {
    onRegister: function () {
      this.$root.$emit("onRegister",this.login, this.password)
    },
  },
  data : () => {
    return {
      login: "",
      password : "",
      error : ""
    }
  },
}
</script>

<style scoped>

</style>