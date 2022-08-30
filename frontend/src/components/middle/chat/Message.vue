<template>
  <div>
    <div class="container darker" v-if="message.sender === user">
      <p>{{message.content}}</p>
      <img src="@/assets/favicon.jpg" alt="Avatar" class="right">
    </div>
    <div class="container" v-if="message.sender !== user">
      <img src="@/assets/favicon.jpg" alt="Avatar">
      <p>{{message.content}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: ["message", "user"]
}
</script>

<style scoped>
.container {
  border: 2px solid #dedede;
  background-color: #f1f1f1;
  border-radius: 5px;
  padding: 10px;
  margin: 10px 0;
}

/* Darker chat container */
.darker {
  border-color: #ccc;
  background-color: #bbbbbb;
}

/* Clear floats */
.container::after {
  content: "";
  clear: both;
  display: table;
}

/* Style images */
.container img {
  float: left;
  max-width: 50px;
  width: 100%;
  margin-right: 20px;
  border-radius: 50%;
}

/* Style the right image */
.container img.right {
  float: right;
  margin-left: 20px;
  margin-right:0;
}

/* Style time text */
.time-right {
  float: right;
  color: #aaa;
}

/* Style time text */
.time-left {
  float: left;
  color: #999;
}
</style>