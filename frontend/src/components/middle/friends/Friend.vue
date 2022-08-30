<template>
<tr v-on:click="onFriend">
  <td>{{friend.id}}</td>
  <td>{{friend.login}}</td>
</tr>
</template>

<script>
export default {
  name: "Friend",
  props:["friend"],
  methods: {
    onFriend : function () {
      this.$root.$emit("onFriend", this.friend.login)
    }
  }
}
</script>

<style scoped>
tr :hover {
  background-color: #2c3e50;
}
</style>