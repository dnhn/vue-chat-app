<template>
  <div>
    <img src="@/assets/img/profile.jpg" alt="">
    <span class="name">{{person.name}}</span>
    <span class="time">{{person.time}}</span>
    <span class="preview">{{person.preview}}</span>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  props: ['person']
}
</script>

<style scoped></style>
