<template>
  <section id="education" class="hello">
    <h2>Education</h2>
    <div v-for="school in schools" :key="school.id">
      <h3 class="title">{{ school.title.rendered }}</h3>
      <h4 class="dates">{{ formatDate(school.acf.start_date) }} - {{ formatDate(school.acf.graduation_date) }}</h4>
      <h4 class="degree">{{ school.acf.degree }} degree in {{ school.acf.area_of_study }}</h4>
    </div>
  </section>
</template>

<script>
import dayjs from 'dayjs';

export default {
  name: 'Education',
  props: {
    sectionHeading: String
  },
  methods: {
    formatDate(dateString) {
      const date = dayjs(dateString);
      // Then specify how you want your dates to be formatted
      return date.format('MMM YYYY');
    }
  },
  data() {
    return {
      schools: null
    };
  },
  created() {
    const url = 'http://localhost:8888/headless-portfolio/wp-json/wp/v2/schools?filter[orderby]=date&order=asc';
    // Simple GET request using fetch
    fetch(url)
      .then(response => response.json())
      .then(response => (this.schools = response))
      .catch(err => {
        console.log(err.message || err);
        this.schools = false
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
    content: 'Education';
    position: absolute;
    top: .1em;
    left: 0;
    z-index: 1;
    color: $dark;
  }
}

</style>
