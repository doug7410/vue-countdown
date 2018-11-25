<template>
  <div id="app" :style="{backgroundImage: `url('/img/${this.image}')`}">
    <div class="description">
      <h3>{{ destination }} - {{ tripDate }}</h3>
    </div>
    <div class="clock-container">
      <clock :date="date"/>
    </div>
  </div>
</template>

<script>
  import Clock from './components/Clock.vue'

  export default {
    name: 'app',
    data() {
      return {
        destination: 'New Zealand',
        date: 'Tue Nov 25 2018 10:00:00 GMT-0400 (Eastern Daylight Time)',
        image: 'new-zealand-2.jpg',
        images: [
          'new-zealand-2.jpg',
          'new-zealand-3.jpg',
          'new-zealand-4.jpg',
          'new-zealand-5.jpg',
          'new-zealand-6.jpg',
          'new-zealand-8.jpg',
          'new-zealand-9.jpg',
          'new-zealand-10.jpg',
          'new-zealand-11.jpg',
          'new-zealand-12.jpg'
        ]
      }
    },
    created() {
      setInterval(() => {
        this.setImage()
      }, 12000)
    },
    components: {
      Clock
    },
    methods: {
      setImage() {
        const currentImageIndex = this.images.indexOf(this.image)
        const lastImageIndex = this.images.length - 1

        if (currentImageIndex === lastImageIndex) {
          this.image = this.images[0]
        } else {
          this.image = this.images[currentImageIndex + 1]
        }
      }
    },
    computed: {
      tripDate() {
        const date = new Date(this.date)
        return date.toLocaleDateString() +  ' - ' + date.toLocaleTimeString()
      }
    }
  }
</script>

<style lang="scss">
  @import "./scss/main";

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    /*background-image: url("assets/new-zealand-3.jpg");*/
    background-size: cover;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    align-items: center;
    flex-direction: column;
    background-color: black;
  }

  .clock-container {
    width: 100%;
  }

  .description {
    font-size: 1.1rem;
    color: #263238;
  }
</style>
