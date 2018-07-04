<template>
  <div class="right">
    <div class="top">
      <span>To:
        <span class="name">Thomas Bangalter</span>
      </span>
    </div>
    <div class="chat active-chat">
      <div class="conversation-start">
        <span>Today, 6:48 AM</span>
      </div>
      <div
        class="bubble"
        :class="{
          'me': msg.sender === 'me',
          'you': msg.sender === 'you'
        }"
        v-for="(msg, index) in messages"
        :key="index">
        {{msg.text}}
      </div>
    </div>
    <div class="write">
      <a href="javascript:;" class="write-link attach"></a>
      <input
        type="text"
        placeholder="Your message here"
        v-model="newMessage.text"
        @keypress.enter="sendMessage" autofocus />
      <a href="javascript:;" class="write-link smiley"></a>
      <a class="write-link send"
         @click="sendMessage"></a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ChatBox',
  props: ['contacts'],
  data () {
    return {
      newMessage: {
        text: '',
        sender: 'me'
      },
      messages: [
        {
          text: 'Hello world!',
          sender: 'me',
          time: ''
        },
        {
          text: 'How are you?',
          sender: 'me',
          time: ''
        }
      ]
    }
  },
  methods: {
    sendMessage () {
      if (this.newMessage.text) {
        this.messages.push(this.newMessage)
        this.newMessage = {
          text: '', sender: 'me'
        }
        setTimeout(this.respond, 2000)
      }
    },
    respond () {
      this.messages.push({
        text: 'Thank you for your message',
        sender: 'you'
      })
    }
  }
}
</script>

<style scoped>

</style>
