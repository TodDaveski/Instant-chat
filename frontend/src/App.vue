<template>
  <div id="app">
    <Header :user="user"/>
    <img alt="Vue logo" src="./assets/logo.png">
    <Middle :user="user"/>
  </div>
</template>

<script>

import axios from "axios";
import Header from "@/components/Header";
import Middle from "@/components/Middle";

export default {
  name: 'App',
  data: function () {
    return {
      user : "",
      friend : "",
      componentKey : false,
      showChat : false,
    }
  },
  beforeCreate() {
    this.$root.$on("onEnter", (login, password) => {
      axios.post("/api/1/jwt",{
        "login": login,
        "password": password
      }).then(response => {
        localStorage.setItem("jwt", response.data)
        axios.get("/api/1/user", {
          params : {
            jwt : response.data
          }
        }).then(response => {
          this.user = response.data
        })
      }).catch((error) => this.$root.$on("onEnterError", error))
    });
    this.$root.$on("onRegister", (login, password) => {
      axios.post("/api/1/register", {
        "login" : login,
        "password" : password
      }).then(response => {
        if (response.status === 200) {
          this.$root.$emit("onChangePage", "Login")
        }
      })
    })
  },
  beforeMount() {
    if (localStorage.getItem("jwt") && !this.user) {
      axios.get("/api/1/user", {
        params : {
          jwt : localStorage.getItem("jwt")
        }
      }).then(response => this.user = response.data)
    }
  },
  components:{
    Header,
    Middle
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
