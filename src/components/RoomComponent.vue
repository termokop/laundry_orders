<script setup>

import { ref } from 'vue';
defineProps({
  roomNumber: {
    type: String,
    required: true
  }
})

let status = ref("None")
    


function changeStatus(value) {
  status.value = value
  console.log(status.value)
}
</script>

<template>
  <div class="room">
    <div class="room-number">{{ roomNumber }}</div>
    <div class="room-status">
      <div
        class="btn-status"
        :class="status == 'None' ? 'choosen-btn-status' : ''"
        @click="changeStatus('None')"
      >
        None
      </div>
      <div
        class="btn-status"
        :class="status == 'Stay Over' ? 'choosen-btn-status' : ''"
        @click="changeStatus('Stay Over')"
      >
        Stay Over
      </div>
      <div
        class="btn-status"
        :class="status == 'Check Out' ? 'choosen-btn-status' : ''"
        @click="changeStatus('Check Out')"
      >
        Check Out
      </div>
    </div>
  </div>
</template>

<style scoped>
.room {
    width: 100%;
    background-color: aliceblue;
    margin-bottom: 5px;
}
.room-number {
    display: flex;
    justify-content: center;
    color: green;
    font-size: x-large;
}
.room-status {
  width: 300px;
  display: flex;
  justify-content: space-between;
  background-color: #adffda;
  cursor: pointer;
}
.btn-status {
  width: 30%;
}

.choosen-btn-status {
  background-color: lightgreen;
}
</style>
