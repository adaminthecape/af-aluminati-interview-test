<template>
  <div>
    {{/** Changed very long line to readable XML style **/}}
    <div class="number"
         :id="'number-'+number"
         v-for="number in this.getNumbers()"
         :key="'n-'+number"
         @mouseover="highlightDivisors(number)"
         @mouseout="reset">
      {{number}}
    </div>
  </div>
</template>

<script>
  export default {
    /** Added 'name' prop **/
    name: 'Numbers',
    data() {
      return {
        limit: this.$parent.limit,
        /** numbers was never used; now is used **/
        numbers: []
      }
    },
    watch: {
      /** changed syntax to inline-bracket **/
      ['$parent.limit'](newLimit) {
        this.limit = newLimit;
      }
    },
    methods: {
      /** Renamed n() and hov() to something more descriptive **/
      getNumbers() {
        let numbers = [];
        /** changed var to let **/
        for ( let i = 0; i < this.limit; i++ ) {
          // numbers = [...numbers, i];
          /** changed to push **/
          numbers.push(i);
        }
        let result = numbers.sort(() => Math.random() - 0.5);
        /**
         * Now putting the numbers into the existing
         * this.numbers array so it can be available
         * without extra unnecessary computations.
         **/
        this.numbers = result;
        // this.$set( this.numbers, 0, result );
        return result;
      },
      /** Renamed n() and hov() to something more descriptive **/
      highlightDivisors(number) {
        /** changed to get data more efficiently **/
          // const nums = document.querySelectorAll('.number');
        const nums = this.numbers;
        /** initialize divisors array **/
        let divisors = [];

        /** changed for loop to for-of **/
        for ( let num of nums ) {
          /** changed from getting/trimming text to just getting the number **/
          if ( number % num === 0 ) {
            /** added semicolons **/
            document.getElementById('number-' + num).classList.add('active');
            /** add to divisors array **/
            divisors.push(num);
          }
        }
        /** logging divisors afterward for readability **/
        /** nobody was going to be able to read up to 100+ console lines coherently **/
        console.log('divisors:', divisors.toString());
      },
      reset() {
        const nums = document.querySelectorAll('.number');
        /** added semicolon **/
        nums.forEach(num => num.classList.remove('active'));
      },
      mounted: function() {
        this.setNumbers();
      }
    }
  }
</script>

<style scoped>
  .number {
    display: inline-block;
    padding: 5px;
    background-color: lightgrey;
    margin: 5px;
  }
  .active {
    background-color: red;
  }
</style>
