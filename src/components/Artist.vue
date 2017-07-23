<template>
  <li class="artist">
    <h2>
      <a :href="artist.url" target="_blank">{{ artist.name }}</a>
    </h2>
    <img :src="artist.image[3]['#text']" :alt="artist.name" />
    <div class="listeners">
      <p> {{ artist.listeners }} reproducciones </p>
    </div>
  </li>
</template>

<script>
export default {
  name: 'artist',
  props: [ 'artist' ]
}
</script>

<style lang="stylus" scoped>
li.artist
 display inline-block
 padding 5px
 margin 10px
 border 2px solid #41b883
 border-radius 5px
li.artist a
  text-decoration none
li.artist p
  background-color #41b883
  color #FFFFFF
  margin 0
  padding 10px 10px
</style>
