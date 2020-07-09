<template>
  <div class="socket">
    <div class="box">
      <ul v-for="(item, index) in data" :key="index">
        <li>{{item}}</li>
      </ul>
    </div>
    <div class="send-message">
      <input type="text" v-model="message" />
      <button @click="sendMessage">gửi</button>
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client';
const socket = io('localhost:3001')
export default {
  data() {
    return {
      data: [],
      message: "",
    };
  },
  created() {
      socket.on('chat message', data => {
          this.data.push(data)
      })
  },
  methods: {
    sendMessage() {
        socket.emit('chat message', this.message);
        this.message= ''
    },
  },
};
</script>

<style lang="scss" scoped>
.socket {
  .box {
    margin: 10px auto;
    width: 500px;
    height: 400px;
    border: 1px solid black;
    ul {
        li{
            list-style: none;
        }
    }
  }
  .send-message {
    input {
      margin-left: 410px;
      width : 462px;
    }
  }
}
</style>
