<template>
  <div>
    <div>
      <p>User input (<span style="font: 10px">numbers only</span>)</p>
      <input type="text" v-model="userInput" style="width: 200px; margin-right: 10px" />
      <button @click="findProfit" style="padding: 0 20px">Find</button>
    </div>
    <div style="margin-top: 20px">
      <p>
        Profit: <span style="font: 12pt; font-weight: bold">{{ maxProfit }}</span>
      </p>
      <p>
        T: <span style="font: 12pt; font-weight: bold">{{ solution.T }}</span>
      </p>
      <p>
        P: <span style="font: 12pt; font-weight: bold">{{ solution.P }}</span>
      </p>
      <p>
        C: <span style="font: 12pt; font-weight: bold">{{ solution.C }}</span>
      </p>
    </div>
  </div>
</template>
<script setup>
import { ref, reactive } from 'vue'
const userInput = ref()

const solution = ref({ T: 0, P: 0, C: 0 })
const maxProfit = ref(0)

const buildings = reactive([
  {
    type: 'T',
    time: 5,
    profit: 1500,
  },
  {
    type: 'P',
    time: 4,
    profit: 1000,
  },
  {
    type: 'C',
    time: 10,
    profit: 2000,
  },
])

const findProfit = () => {
  let n = Number(userInput.value)
  if (n == '') {
    alert('User input is blank')
  }
  solution.value = { T: 0, P: 0, C: 0 }
  maxProfit.value = 0

  function findSolution(remaining, counts, current) {
    if (current > maxProfit.value) {
      maxProfit.value = current
      solution.value = { ...counts }
    }
    for (let item of buildings) {
      if (remaining >= item.time) {
        const opTime = remaining - item.time
        const profit = opTime * item.profit

        counts[item.type]++

        findSolution(remaining - item.time, counts, current + profit)

        counts[item.type]--
      }
    }
  }
  findSolution(n, { T: 0, P: 0, C: 0 }, 0)
}
</script>
