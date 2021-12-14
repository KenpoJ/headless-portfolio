<template>
  <section id="work-history" class="hello">
    <h2>Work History</h2>
    <div class="flex">
      <div v-for="position in positions" :key="position.id" class="position-container">
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
    content: 'Work History';
    position: absolute;
    top: .1em;
    left: 0;
    z-index: 1;
    color: $dark;
  }
}

.position-container {
  margin: 0 auto;
  // padding: 1rem 1rem 1.5rem;
  flex: 1 1 90%;
  @include box-shadow();
  @include border-radiuses(20%, 50%, 20%, 50%);

  .title,
  .company,
  .dates {
    text-align: center;
  }
  .title {
    margin-bottom: .7em;
    font-size: 1.5rem;
    color: $offDark;
  }
  .dates {
    font-size: .9rem;
  }

  @media screen and (min-width: 500px) and (max-width: 1024px) {
    flex: 0 1 47%;
  }
  @media screen and (min-width: 1025px) {
    flex: 0 0 30%;
  }
}
</style>
