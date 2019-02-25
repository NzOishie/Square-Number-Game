<template xmlns:v-model="http://www.w3.org/1999/xhtml">
  <div>
    <div>
      <form v-on:submit.prevent="onSubmit">
        <div class="row" >
          <div class="col-md-1">
            <!--Generates random number-->
            <label> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{{number}}</label>
          </div>
          <div class="col-md-11">
             <!--Takes the input and disables when 10 seconds are over -->
            <input  v-model.number="result" v-on:keyup="checkResult" type="number" :disabled=isDisabled>
            <!--Checks the answer is correct or not-->
            <label class="green" v-if="Math.sqrt(this.result) === this.number"> &nbsp;&nbsp;Correct </label>
            <label class="red" v-else>&nbsp;&nbsp; Wrong </label>
          </div>
        </div>
        <br>
        <br>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    time_count: {
      type: Number
    }
  },
  data: function () {
    return {
      number: this.randomNumber(),
      result: ''
    }
  },
  methods: {
    randomNumber: function () {
      return Math.floor(Math.random() * 50) + 1
    },
    checkResult: function (event) {
      if (Math.sqrt(this.result) >= this.number) {
        this.$emit('checkResult', 1)
        return true
      } else {
        this.$emit('checkResult', 0)
        return false
      }
    }

  },
  computed: {
    isDisabled () {
      if (this.time_count <= 0) {
        return true
      }
    }
  }
}
</script>

<style>
  .green{
    color: forestgreen;
  }
  .red{
    color: red;
  }

</style>
