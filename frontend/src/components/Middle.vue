<template>
  <div>
  <Login v-if="page === 'Login'"/>
  <Register v-if="page === 'Register'"/>
  <FriendList v-if="page === 'FriendList'" :user="user"/>
  <Chat v-if="page === 'Chat'" :friend="friend" :user="user"/>
  </div>
</template>
<script>
import Login from "@/components/middle/Login";
import FriendList from "@/components/middle/friends/FriendList";
import Register from "@/components/middle/Register";
import Chat from "@/components/middle/chat/Chat";

export default {
  name: "Middle",
  components: {Chat, Register, FriendList, Login},
  props:["user"],
  data : function () {
    return {
      page : 'Login',
      friend : ""
    }
  },
  mounted() {
    this.$root.$on("onChangePage", (page) => {
        this.page = page;
    });
    this.$root.$on("onFriend", (friend) => {
      this.friend = friend
      this.page = "Chat"
    });
  },

  //TODO : add some proper routing
}
</script>

<style scoped>

</style>