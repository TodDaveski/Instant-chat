<template>
  <header>
<div id="navigation">
  <ul>
    <li><a href="#" @click.prevent="changePage('Login')">Login</a></li>
    <li><a href="#" @click.prevent="changePage('Register')">Register</a></li>
    <li><a href="#" @click.prevent="changePage('FriendList')">Friends</a></li>
    <li><a> {{user}} </a></li>
  </ul>
</div>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: ["user"],
  methods:{
    changePage : function (page) {
      this.$root.$emit("onChangePage", page)
    }
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
}

li {
  float: left;
}

li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

li a:hover {
  background-color: #111;
}
.active {
  background-color: #04AA6D;
}
#navigation {
  margin-bottom: 20px;
}
</style>