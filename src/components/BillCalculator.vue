<script lang="ts">
  import { defineComponent, ref, computed, watch } from "vue";

  export default defineComponent({
    name: "BillCalculator",
    setup(){
      
      const price = ref<number | null>(null);
      const tip = ref<number | null>(null);
      const currency = ref<string>("USD");

      const currencies = {
        usd: "$",
        php: "₱",
        yen: "¥",
      };

      
      const total = computed(() => {
        return (price.value || 0) + (tip.value || 0);
      });

      
      const totalFormat = computed(() => {
        const symbol = currencies[currency.value.toLowerCase()];
        return `${symbol} ${total.value.toFixed(2)}` ;
      });

     
      const resetInputs = () => {
        price.value = null;
        tim.value = null;
      };

    
      const totalColor = computed(() => {
        if(total.value < 100) {
          return "red";
        } else if (total.value > 999) {
          return "green"
        } 

        return "black";
      });

      return{
        price,
        tip,
        currency,
        currencies,
        total,
        totalFormat,
        resetInputs,
        totalColor,
      }

    },
  });
</script>

<template>
  <div class="bill-calculator">
    <div class="input-group">
      <label for="currency">Currency:</label>
      <select v-model="currency" @change="resetInputs">
        <option v-for="(symbol, key) in currencies" :key ="key" :value="key">
          {{key.toUpperCase()}}
        </option>
      </select>
    </div>

    <div class="input-group">
      <label for="price">Price:</label>
      <input type="number" v-model="price" placeholder="Enter Price" />
    </div>

    <div class="input-group">
      <label for="tip">Tip:</label>
      <input type="number" v-model.number="tip" placeholder="Enter Tip" />
    </div>

    <div :style="{ color: totalColor }" class="total-display">
      Total: {{totalFormat}}
    </div>

  </div>
</template>

<style scoped>
.bill-calculator {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 2px solid  #33f9ff;
  border-radius: 5px;
  background: #353535;
}

.input-group {
  margin-bottom: 10px;
}

.input-group label {
  margin-right: 10px;
}

.total-display {
  font-size: 1.5em;
  font-weight: bold;
  margin-top: 20px;
}

label{
  color: #33f9ff;
}
</style>
