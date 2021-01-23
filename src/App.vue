<template>
  <Header :totalIncome="state.totalIncome" />
  <Form  @add-income="AddIncome" />
  <IncomeList state="state" />
</template>

<script>
import { reactive,computed } from 'vue';
import Header from './components/Header';
import Form from './components/Form';
import IncomeList from './components/IncomeList';


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

    function AddIncome(data){
      let dateSplit = data.date.split("-");
      let newDate = new Date(dateSplit[0],dateSplit[1],dateSplit[2]);

      state.income = [...state.income, {
        id: Date.now(),
        desc : data.desc,
        value : parseInt(data.value),
        date : newDate.getTime()


      }]

    }

    return {
      Header,
      IncomeList,
      Form,
      state,
      AddIncome
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
