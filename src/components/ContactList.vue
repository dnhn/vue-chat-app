<template>
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
        <Contact :person="person" />
      </li>
    </ul>
  </div>
</template>

<script>
import Contact from './Contact'

export default {
  name: 'ContactList',
  components: { Contact },
  props: ['contacts'],
  data () {
    return {
      activeUser: 0
    }
  },
  methods: {
    selectContact (index) {
      this.activeUser = index
    }
  }
}
</script>

<style scoped>

</style>
