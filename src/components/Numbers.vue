<template>
  <div>
    <div class="number" :id="'number-'+number" v-for="number in generateRandomNumberArray()" :key="number" @mouseover="highlightNumbersDivisors(number)" @mouseout="resetHighligtedNumbers">
      {{number}}
    </div>
  </div>
</template>

<script>
/* 
  Gave more descriptive names to functions - for easier debugging and refactoring
*/
export default {
  data()
  {
    return {
      limit: this.$parent.limit,
      //numbers array variable not used
    }
  },
  watch: {
    ['$parent.limit'](newLimit)
    {
      this.limit = newLimit;
    }
  },
  methods: {
    generateRandomNumberArray() //initialise random numbers
    {
      let numbersArray = [];
      //loop starting at 1 and ending with this.limit
      for( let i = 1 ; i <= this.limit ; i++ )
      {
        //add value to current array
        //instead of creating new array and reasigning array to numbersArray
        numbersArray.push(i);
      }
      return numbersArray.sort(() => Math.random() - 0.5); //randomise array
    },
    highlightNumbersDivisors(number) //hover function - numbers' divisors
    {
      /*
        no need to loop through all of the numbers to find the divisors
        used element id to directly find divisor element and highlight element
       */
      //loop from 1 to number
      for( let i = 1 ; i < number ; i++ )
      {
        if(number % i === 0) //find divisor
          document.querySelector(`#number-${i}`)
          .classList.add('active'); //highlight divisor element
      }
    },
    resetHighligtedNumbers()
    {
      //get all elements with class names number and active to ensure that when active is removed it does exist
      document.querySelectorAll('.number.active')
      .forEach(numberElement => {
        numberElement.classList.remove('active'); //remove class active from element
      });
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
