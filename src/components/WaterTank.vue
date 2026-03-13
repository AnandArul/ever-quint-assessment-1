<template>
  <div>
    <div>
      <p>User input (<span style="font: 10px">input like 3,2,5,0,8,0</span>)</p>
      <input type="text" v-model="userInput" style="width: 200px; margin-right: 10px" />
      <button @click="setArray" style="padding: 0 20px">Find</button>
    </div>
    <div style="margin-top: 20px">
      Total Water units:
      <span style="font-size: 14pt; font-weight: bold">{{ totalUnits }}</span>
    </div>
    <table>
      <tr v-for="(item, index) in result" :key="index">
        <td
          v-for="value in item"
          :key="value"
          style="width: 100px; height: 40px; border: 1px solid #dddddd; padding: 0"
          :style="{ background: value }"
        ></td>
      </tr>
    </table>
  </div>
</template>
<script setup>
import { ref, reactive } from 'vue'

let userInput = ref('3, 0, 4, 0, 0, 0, 6, 0, 6, 4, 0')
const inputWatertankArray = ref([])
let arrayLength = ref(0)
let totalUnits = ref(0)

let result = reactive([])

const setArray = () => {
  result = []
  totalUnits.value = 0

  if (userInput.value.trim() == '') {
    alert('User input is blank')
  }

  inputWatertankArray.value = userInput.value.split(',').map(Number)
  arrayLength.value = inputWatertankArray.value.length

  let startMax = reactive([])
  let endMax = reactive([])

  for (const [index, val] of inputWatertankArray.value.entries()) {
    if (index === 0) {
      startMax[0] = val
    } else {
      startMax[index] = Math.max(startMax[index - 1], val)
    }
  }

  endMax[arrayLength.value - 1] = inputWatertankArray.value.at(-1)

  for (let i = arrayLength.value - 2; i >= 0; i--) {
    endMax[i] = Math.max(endMax[i + 1], inputWatertankArray.value[i])
  }

  let waterArray = new Array(arrayLength.value).fill(0)
  for (let i = 0; i < arrayLength.value; i++) {
    let a = Math.min(startMax[i], endMax[i]) - inputWatertankArray.value[i]
    waterArray[i] = a > 0 ? a : 0
  }

  const maxHeight = Math.max(...inputWatertankArray.value.map((h, i) => h + waterArray[i]))
  for (let row = maxHeight; row > 0; row--) {
    const rowArray = []
    for (let col = 0; col < arrayLength.value; col++) {
      if (inputWatertankArray.value[col] >= row) {
        rowArray.push('yellow')
      } else if (inputWatertankArray.value[col] + waterArray[col] >= row) {
        totalUnits.value++
        rowArray.push('blue')
      } else {
        rowArray.push('white')
      }
    }
    result.push(rowArray)
  }
}
</script>
