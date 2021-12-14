<template>
  <nav class="nav">
    <div class="container">
      <div class="nav-item">
        <a class="nav-link" href="#">About</a>
      </div>
      <div class="nav-item">
        <a class="nav-link" href="#">Skills</a>
      </div>
      <div class="nav-item">
        <a class="nav-link" href="#education">Education</a>
      </div>
      <div class="nav-item">
        <a class="nav-link" href="#work-history">Work History</a>
      </div>
      <div class="nav-item">
        <a class="nav-link" href="#projects">Projects</a>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Nav',
  props: {
    sectionHeading: String
  },
  data() {
    return {
      
    };
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
