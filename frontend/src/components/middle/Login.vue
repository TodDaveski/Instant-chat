<template>
  <div id="Login">
    <h1>
      Login
    </h1>
  <form method="post" @submit.prevent="onEnter">
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
  name: "Login",
  methods: {
    onEnter: function () {
      this.$root.$emit("onEnter",this.login, this.password)
    },
  },
  beforeCreate() {
    this.$root.$on("onEnterError", error => this.error = error)
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
input {
  margin-right: 15px;
}
.error {
  margin-top: 10px;
  color: red;
}
</style>