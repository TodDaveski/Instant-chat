<template>
<div>
  <Message v-for="msg in messages" :message="msg" :user="user" :key="msg.id"/>
  <div>
    <form @submit.prevent="sendMessage">
      <label> New Message</label>
      <input type="text" v-model="newMessage">
      <input type="submit">
    </form>
  </div>
</div>
</template>

<script>
import axios from "axios";
import Message from "@/components/middle/chat/Message";

export default {
  components: {Message},
  data : () => {
    return {
      messages : [],
      newMessage : "",
      conn : null
    }
  },
  name: "Chat",
  props:["user", "friend"],
  methods: {
    sendMessage: function () {
      let message = {
        content : this.newMessage,
        sender : this.user,
        recipient : this.friend
      }
      this.messages.push(message)
      this.conn.send(JSON.stringify(message))
      axios.post("/api/1/sendMessage", {
        "sender" : this.user,
        "recipient" : this.friend,
        "content" : this.newMessage
      })
    }
  },
  created() {

  },
  beforeMount() {
    this.conn = new WebSocket("ws://localhost:8090/ws?login=" + this.user)
    this.conn.onmessage = (evt) => {
      let message = JSON.parse(evt.data)
      this.messages.push(message)
    }
    axios.post("/api/1/chat", {
        "user" : this.user,
        "friend" : this.friend
      }
    ).then(response => {
      this.messages = response.data
    })
  }
}
</script>

<style scoped>

</style>