<template>
  <div style="margin: 20px 0">
    <h3 style="margin-bottom: 10px; font-size: 1.5rem; font-weight: 600">Solution</h3>
    <div style="display: flex; gap: 20px">
      <div class="radio-group">
        <input type="radio" id="one" value="max_profit" v-model="picked" />
        <label for="one">Max Profit</label>
      </div>
      <div class="radio-group">
        <input type="radio" id="two" value="water_tank" v-model="picked" />
        <label for="two">Water Tank</label>
      </div>
    </div>
    <div style="margin-top: 20px">
      <div v-if="picked == 'max_profit'">
        <MaxProfit />
        <!-- <div>Max Profit</div> -->
      </div>
      <div v-if="picked == 'water_tank'">
        <WaterTank />
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, defineAsyncComponent } from 'vue'
const WaterTank = defineAsyncComponent(() => import('@/components/WaterTank.vue'))
const MaxProfit = defineAsyncComponent(() => import('@/components/MaxProfit.vue'))

const picked = ref('One')

// const handlePick = (value) => {
//   picked.value = value
// }
</script>

<style scoped>
.radio-group {
  display: flex;
  align-items: center;
  gap: 5px;
}
</style>
