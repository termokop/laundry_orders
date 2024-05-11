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
  width: 100%;
  display: flex;
  justify-content: space-between;
  cursor: pointer;
}
.btn-status {
  width: 30%;
  padding: 2px;
  border: black 1px solid;
  background-color: #adffda;
}

.choosen-btn-status {
  background-color: lightgreen;
}
</style>
