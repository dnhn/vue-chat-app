<template>
  <div class="wrapper">
    <div class="container">
      <div class="left">
        <div class="top">
          <input type="text" />
          <a href="javascript:;" class="search"></a>
        </div>
        <ul class="people">
          <li
            class="person"
            v-for="(person, index) in contacts"
            :key="index"
            :class="{'active': index === activeUser}"
            @click="selectContact(index)">
            <img src="@/assets/img/profile.jpg" alt="">
            <span class="name">{{person.name}}</span>
            <span class="time">
              {{person.messages.length ? person.messages[person.messages.length - 1].time : ''}}
            </span>
            <span class="preview">
              {{person.messages.length ? person.messages[person.messages.length -1].text : ''}}
            </span>
          </li>
        </ul>
      </div>
      <div class="right">
        <div class="top">
          <span>To:
              <span class="name">{{contacts[activeUser].name}}</span>
          </span>
        </div>
        <div class="chat active-chat">
          <div class="conversation-start" v-if="contacts[activeUser].messages.length">
            <span>{{contacts[activeUser].messages[0].time}}</span>
          </div>
          <div
            class="bubble"
            :class="{
              'me': msg.sender === 'me',
              'you': msg.sender === 'you'
            }"
            v-if="contacts[activeUser].messages.length"
            v-for="(msg, index) in contacts[activeUser].messages"
            :key="index">
            {{msg.text}}
          </div>
        </div>
        <div class="write">
          <a href="javascript:;" class="write-link attach"></a>
          <input
            type="text"
            placeholder="Your message here"
            ref="inputMessage"
            v-model="newMessage.text"
            @keypress.enter="sendMessage" autofocus />
          <a href="javascript:;" class="write-link smiley"></a>
          <a class="write-link send"
             @click="sendMessage"></a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      activeUser: 0,
      contacts: [
        {
          name: 'Evan You',
          messages: [
            {
              text: 'Welcome to Vue.js',
              time: '19:00',
              sender: 'you'
            }
          ]
        },
        {
          name: 'Mark Evans',
          messages: [
            {
              text: 'Thank you very much!',
              time: '23:09',
              sender: 'you'
            },
            {
              text: 'My pleasure.',
              time: '23:20',
              sender: 'me'
            }
          ]
        },
        {
          name: 'Momcilo Popov',
          messages: [
            {
              text: 'Hi there!',
              time: '21:00',
              sender: 'me'
            },
            {
              text: 'Nice to meet you!',
              time: '21:10',
              sender: 'you'
            }
          ]
        }
      ],
      newMessage: {
        text: '',
        time: '',
        sender: 'me'
      }
    }
  },
  methods: {
    selectContact (index) {
      this.activeUser = index
      this.$refs.inputMessage.focus()
    },
    sendMessage () {
      const activeIndex = this.activeUser

      if (this.newMessage.text) {
        this.newMessage.time = newDateTime()
        this.contacts[activeIndex].messages.push(this.newMessage)
        this.newMessage = {
          text: '',
          time: '',
          sender: 'me'
        }
        setTimeout(() => this.respond(activeIndex), 2000)
      }
    },
    respond (index) {
      this.contacts[index].messages.push({
        text: 'Thank you for your message',
        time: newDateTime(),
        sender: 'you'
      })
    }
  }
}

function newDateTime () {
  let date = new Date()
  const hour = date.getHours()
  const minute = date.getMinutes()

  return `${hour >= 10 ? hour : `0${hour}`}:${minute >= 10 ? minute : `0${minute}`}`
}
</script>

<style scoped></style>
