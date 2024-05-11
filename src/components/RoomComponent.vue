<script setup>
defineProps({
  roomObj: {
    type: Object,
    required: true
  }
})

</script>

<template>
  <div class="room">
    <div class="room-number">{{ roomObj.room_number }}</div>
    <div class="room-status">
      <div
        class="btn-status"
        :class="roomObj.status == 'None' ? 'choosen-btn-status' : ''"
        @click="$emit('changeStatus',roomObj.room_number, 'None')"
      >
        None
      </div>
      <div
        class="btn-status"
        :class="roomObj.status == 'Stay Over' ? 'choosen-btn-status' : ''"
        @click="$emit('changeStatus',roomObj.room_number, 'Stay Over')"
      >
        Stay Over
      </div>
      <div
        class="btn-status"
        :class="roomObj.status == 'Check Out' ? 'choosen-btn-status' : ''"
        @click="$emit('changeStatus',roomObj.room_number, 'Check Out')"
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
