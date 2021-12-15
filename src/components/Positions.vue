<template>
  <section id="work-history" class="hello">
    <h2>Work History</h2>
    <div class="flex">
      <div v-for="position in positions" :key="position.id" class="position-container">
        <div class="position-meta">
          <h3 class="title">{{ position.acf.title }} </h3>
          <h4 class="company">{{ position.title.rendered }}</h4>
          <div v-if="position.acf.start_date">
            <h4 class="dates">{{ formatDate(position.acf.start_date) }} - {{ formatDate(position.acf.end_date) }}</h4>
          </div>
        </div>
        <div class="custom-shape-position-topper">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320"><path fill="#292929" fill-opacity="1" d="M0,256L40,250.7C80,245,160,235,240,234.7C320,235,400,245,480,229.3C560,213,640,171,720,149.3C800,128,880,128,960,133.3C1040,139,1120,149,1200,144C1280,139,1360,117,1400,106.7L1440,96L1440,320L1400,320C1360,320,1280,320,1200,320C1120,320,1040,320,960,320C880,320,800,320,720,320C640,320,560,320,480,320C400,320,320,320,240,320C160,320,80,320,40,320L0,320Z"></path></svg>
        </div>
        <div class="position-info">
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
@import '@/scss/variables.scss';
@import '@/scss/mixins.scss';
@import '@/scss/typography.scss';

.position-container {
  margin: 0 auto;
  flex: 1 1 90%;
  display: flex;
  flex-direction: column;

  .position-meta {
    margin-bottom: .2rem;
  }
  .custom-shape-position-topper {
    margin-top: -2rem;
    margin-bottom: -1.1rem;
    padding: 0;
  }
  .position-info {
    margin-top: auto;
    padding: 1.2rem 1.2rem 1.7rem;
    height: 100%;
    color: $light;
    background: $dark;
    @include border-radiuses(0,0,5px,5px);

    &::v-deep {
      .description {
        .tasks {
          padding-left: 1rem;
          list-style-type: disc;

          li {
            padding-bottom: .5rem;
          }
        }
      }
    }
  }
  .title {
    margin-bottom: .2em;
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
