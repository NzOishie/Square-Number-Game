
<template>
  <div  class=" background">
    <div class="container margin">
      <h1 class="blue italic">{{title}}</h1>
      <div class="row">
        <!--Shows the score-->
        <div class="col-md-6">
          <h2 class="green italic">Score : {{count}}</h2>
          {{this.high_score}}
        </div>
        <!--Shows the time count-->
        <div>
          <h3 class="italic" v-if="time_count>0"> Time: <span class="magenta ">{{time_count}}s</span></h3>
          <h3 class="italic" v-if="time_count<=0"> Time: <span class="magenta">0s</span></h3>
        </div>
      </div>
      <!--Shows the component 10 times-->
        <div v-for="n in 10">
          <square-number  v-bind:time_count="time_count"  v-on:checkResult="updateScore($event)" ></square-number>
        </div>
      <!--Button for next trial-->
      <button class="btn btn-info" v-if="time_count <= 0 && this.button < 2" v-on:click="trial_button_count()">
        <a class="white italic" href="/">Try Again?</a>
      </button>
      <!--Button for game over and highest score-->
      <div v-if="time_count <= 0 && this.button >= 2">
        <jumbotron class="jum italic"><h3><b>Game Over!</b></h3></jumbotron>
        <h3 class="italic magenta"> Your highest score is {{this.high_score}}</h3>
      </div>
      <!--Footer-->
      <footer>
        <p class="italic blue">Copyright © 2019</p>
        <p class="blue italic">All rights reserved</p>

      </footer>
    </div>
  </div>
</template>

<script>
import SquareNumber from './SquareNumber'

export default {
  components: {
    'SquareNumber': SquareNumber
  },

  data () {
    return {
      title: 'Lets play the square number game!',
      count: 0,
      time_count: 10,
      button: 0,
      high_score: 0,
      play: false
    }
  },
  methods: {
    updateScore: function (score) {
      if (score === 1) {
        this.count++
      }
    },
    trial_button_count: function () {
      this.button++
      localStorage.setItem('button_click', this.button)
      localStorage.setItem('high_score', this.count)
    }
  },
  created () {
    this.button = localStorage.getItem('button_click')
    if (localStorage.getItem('high_score') > this.high_score) {
      console.log(localStorage.getItem('high_score'))
      this.high_score = localStorage.getItem('high_score')
    }
    window.localStorage.removeItem('button_click')
    window.localStorage.removeItem('high_score')
    let timerId = setInterval(() => this.time_count--, 1000)
    setTimeout(() => { clearInterval(timerId) }, 11000)
  }

}

</script>

<style>
  .jum{
    color: red;
  }
  .white{
    color: white;

  }
  a.hover {
    color: white;
  }
  .blue{
    color: blue;
  }
  .magenta{
    color: darkmagenta;
  }
  .green{
    color: green;
  }
  .italic{
    font-style: italic;
  }
  .background{
    background-image: url("../images/background.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    background-position: right bottom;
    border:none;

  }
  .margin{
    margin-left:37%
  }

</style>
