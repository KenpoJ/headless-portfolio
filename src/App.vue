<template>
  <div id="main" class="content">

    <Hero msg="This is the Hero Area" />

    <Education />
    <Positions />
  </div>
</template>

<script>
import Hero from './components/Hero.vue'
import Education from './components/Education.vue'
import Positions from './components/Positions.vue'

export default {
  name: 'App',
  components: {
    Hero,
    Education,
    Positions
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
