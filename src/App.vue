<template>
  <div id="main" class="content">
    <Nav />
    <Hero msg="Hi! My name is Jason and I'm a Web Developer!" />

    <div class="container content-container">
      <Education />
      <Positions />
      <Projects />
    </div>

    <Footer />

  </div>
</template>

<script>
import Nav from './components/Nav.vue'
import Hero from './components/Hero.vue'
import Education from './components/Education.vue'
import Positions from './components/Positions.vue'
import Projects from './components/Projects.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Nav,
    Hero,
    Education,
    Positions,
    Projects,
    Footer,
  },
  css: {
    loaderOptions: {
      sass: {
        data: `
          @import "@/scss/variables.scss";
          @import "@/scss/mixins.scss";
        `
      }
    }
  }
}
</script>

<style lang="scss">
@import "@/scss/global.scss";
</style>
