<template>
  <div id="countdown">
    <div class="block">
      <div class="number">{{ timeRemaining.days | two_digits }}</div>
      <div class="text">Days</div>
    </div>
    <div class="spacer">:</div>
    <div class="block">
      <div class="number">{{ timeRemaining.hours | two_digits }}</div>
      <div class="text">Hours</div>
    </div>
    <div class="spacer">:</div>
    <div class="block">
      <div class="number">{{ timeRemaining.minutes | two_digits }}</div>
      <div class="text">Minutes</div>
    </div>
    <div class="spacer">:</div>
    <div class="block">
      <div class="number">{{ timeRemaining.seconds | two_digits }}</div>
      <div class="text">Seconds</div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'

  export default{
    data () {
      return {
        timeRemaining: {}
      }
    },
    props: ['date'],
    created () {
      window.setInterval(() => {
        this.timeRemaining = this.getTimeRemaining(this.date)
      }, 1000)
    },
    methods: {
      getTimeRemaining (endtime) {
        const startTime = new Date()
        const total = Date.parse(endtime) - Date.parse(startTime)
        const seconds = Math.floor((total / 1000) % 60).toString()
        const minutes = Math.floor((total / 1000 / 60) % 60).toString()
        const hours = Math.floor((total / (1000 * 60 * 60)) % 24).toString()
        const days = Math.floor(total / (1000 * 60 * 60 * 24)).toString()
        return {
          'total': total,
          'days': days,
          'hours': hours,
          'minutes': minutes,
          'seconds': seconds
        }
      }
    }
  }

  Vue.filter('two_digits', function (value) {
    if (value) {
      if (value.toString().length <= 1) {
        return '0' + value.toString()
      }
      return value.toString()
    }
  })

</script>

<style type="scss">
  #countdown {
    font-family: 'Abel', sans-serif;
    padding: 2em 1em;
    background-color: rgba(21, 26, 62, 0.79);
    color: #fff;
    display: flex;
    justify-content: space-around;
    width: 80%;
    margin: 0 auto;
  }

  .block {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 25%;
  }

  .number {
    font-size: 3em;
  }

  .spacer {
    font-size: 2em;
    align-self: flex-start;
    margin-top: .3em;
  }
</style>
