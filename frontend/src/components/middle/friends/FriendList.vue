<template>
  <div id="FriendsList">
<table>
  <tr>
  <th>User Id</th>
  <th>Username</th>
  </tr>
  <Friend v-for="friend in friends" :friend="friend" :key="friend.id"/>
</table>
  </div>
</template>

<script>
import Friend from "@/components/middle/friends/Friend";
import axios from "axios";
export default {
  name: "FriendList",
  props: ["user"],
  data : () => {
    return {
      friends : []
    }
  },
  components: {Friend},
  beforeMount() {
    axios.get("/api/1/friends", {
          params : {
            user: this.user
          }
        }
    ).then(response => {
      this.friends = response.data
    })
  }
}
</script>

<style scoped>
table,tr, td, th {
  border-collapse: collapse;
}
table,tr, td, th {
  border: 1px solid;
}

</style>