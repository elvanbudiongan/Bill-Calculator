<script lang="ts">
import BillCalculator from './components/BillCalculator.vue' ;
import { defineComponent } from "vue" ;

  export default defineComponent({
    name: "App",
    components: {
      BillCalculator,
    },
  });
</script>

<template>
  <div id="app">
    <h1> Bill Calculator </h1>
    <BillCalculator />
  </div>
</template>

<style scoped>
#app{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 30vh;
}

h1{
  color: #7D9;
}
</style>
