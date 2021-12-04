<template>
  <section id="work-history" class="hello">
    <h1>Work History</h1>
    <div v-for="position in positions" :key="position.id">
      <h3 class="title">{{ position.acf.title }} </h3>
      <h4 class="company">{{ position.title.rendered }}</h4>
      <div v-if="position.acf.start_date">
        <h4 class="dates">{{ formatDate(position.acf.start_date) }} - {{ formatDate(position.acf.end_date) }}</h4>
      </div>
      <div v-if="position.acf.description">
        <div class="description" v-html="position.acf.description "></div>
      </div>
      <div v-if="position.acf.skills">
        <div class="skills">
          {{ position.acf.skills }} 
        </div>
      </div>
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
      positions: null
    };
  },
  created() {
    // HOW DO WE SORT THE RESULTS???
    const url = 'http://localhost:8888/headless-portfolio/wp-json/wp/v2/positions?filter[orderby]=date&order=asc&per_page=100';

    fetch(url)
      .then(response => response.json())
      .then(response => (this.positions = response))
      .catch(err => {
        console.log(err.message || err);
        this.positions = false
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
