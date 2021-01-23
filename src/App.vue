<template>
  <Header :totalIncome="state.totalIncome" />
  <Form />
</template>

<script>
import { reactive,computed } from 'vue';
import Header from './components/Header';
import Form from './components/Form'


export default {
  setup(){
    const state = reactive({
      income : [],
      totalIncome : computed(() => {
        
        let temp = 0;

        if(state.income.length > 0){ //Checking to see if array is empty
          for(let i = 0; i < state.income.length;i++){
            temp += state.income[i].value;
          }

        }
        return temp;

      })
    });

    return {
      Header,
      Form,
      state
    }
  }

  
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

body {
  background: #EEE;
}

</style>
