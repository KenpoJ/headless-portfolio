<template>
  <section id="projects" class="hello">
    <h2>Projects</h2>
    <div v-for="project in projects" :key="project.id">
      <h3 class="title">{{ project.acf.title }} </h3>
      <h4 class="company">{{ project.title.rendered }}</h4>
      
    </div>
  </section>
</template>

<script>
export default {
  name: 'Projects',
  props: {
    sectionHeading: String
  },
  data() {
    return {
      projects: null
    };
  },
  created() {
    // HOW DO WE SORT THE RESULTS???
    const url = 'http://localhost:8888/headless-portfolio/wp-json/wp/v2/projects?filter[orderby]=date&order=asc&per_page=100';

    fetch(url)
      .then(response => response.json())
      .then(response => (this.projects = response))
      .catch(err => {
        console.log(err.message || err);
        this.projects = false
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import '@/scss/global.scss';

h2 {
  // The :after is the main dark colored heading
  margin: 2rem 0 1rem;
  padding: 1rem 0 1rem 1rem;
  position: relative;
  font-size: 2rem;
  color: $light;

  &:after {
    content: 'Projects';
    position: absolute;
    top: .1em;
    left: 0;
    z-index: 1;
    color: $dark;
  }
}

</style>
