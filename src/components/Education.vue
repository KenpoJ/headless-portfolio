<template>
  <section id="education" class="hello">
    <h1>Education</h1>
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
  el: 'education',
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
<style scoped>
h3 {
  margin-bottom:  0;
}
h4 {
  margin:  0 0 .3rem 0;
}
</style>
