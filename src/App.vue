<template>
  <div id="app">
    <Cont>
      <ChatWindow @send-message="sendMessage">
        <ChatMessage v-for="message in data" :key="message.id" :username="message.author" :datetime="message.text"></ChatMessage>
      </ChatWindow>>
    </Cont>
  </div>
</template>

<script>
import axios from 'axios'
import Cont from './components/Container.vue'
import ChatMessage from './components/ChatMessage.vue'
import ChatWindow from './components/ChatWindow.vue'

export default {
  data(){
    return { 
      data: []
    };
  },
  methods:{
    sendMessage({nickname, message}){
      axios.post('http://188.225.47.187/api/chat/sendmessage.php', {
        author: nickname,
        text: message,
      }).then(response =>{
        console.log(response);
        this.getMessages();
      })
    },
    getMessages(){
      axios.get('http://188.225.47.187/api/chat/getmessages.php')
      .then((response) => {
          this.data = response.data;
          //заполнить дату
      });
    },
  },
  name: 'app',
  components: {
    Cont, ChatMessage, ChatWindow,
  },
  mounted() {
    setInterval(()=>{
      this.getMessages();
    }, 3000)
  
  }
}
</script>

<style>
.container {
  width: 764px;
  margin: auto;
  box-shadow: 0 0 15px 0 #5f5f5f73;
}
body {
  margin: 0;
  background-color: #f9f9fa;
}
</style>