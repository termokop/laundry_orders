<script setup>
import { ref } from 'vue'
import RoomComponent from './components/RoomComponent.vue'
import vTable from './components/vTable.vue'

import { linens_for_checkOut, linens_for_stayOver } from './components/linens_for_rooms'
import { rooms_info } from './components/rooms_info'

let linensNeeded = ref({
  3: { floor: '3' },
  4: { floor: '4' },
  5: { floor: '5' },
  6: { floor: '6' },
  7: { floor: '7' },
  8: { floor: '8' },
  9: { floor: '9' },
  10: { floor: '10' },
  11: { floor: '11' },
  12: { floor: '12' }
})

const hotelData = ref({
  rooms: [...rooms_info],
  changeStatus(room, newStatus) {
    for (let i = 0; i < this.rooms.length; i++) {
      if (this.rooms[i].room_number == room) {
        this.rooms[i].status = newStatus
        break
      }
    }
  }
})

const calculateForFloors = () => {
  linensNeeded.value = {
    3: { floor: '3' },
    4: { floor: '4' },
    5: { floor: '5' },
    6: { floor: '6' },
    7: { floor: '7' },
    8: { floor: '8' },
    9: { floor: '9' },
    10: { floor: '10' },
    11: { floor: '11' },
    12: { floor: '12' }
  }
  hotelData.value.rooms.forEach((currentRoom) => {
    if (currentRoom.status === 'Stay Over') {
      Object.keys(linens_for_stayOver[currentRoom.room_type]).forEach((key) => {
        linensNeeded.value[parseInt(currentRoom.room_number.substring(0, 2)).toString()][key] =
          (linensNeeded.value[parseInt(currentRoom.room_number.substring(0, 2)).toString()][key] ||
            0) + linens_for_stayOver[currentRoom.room_type][key]
      })
    } else if (currentRoom.status === 'Check Out') {
      Object.keys(linens_for_checkOut[currentRoom.room_type]).forEach((key) => {
        linensNeeded.value[parseInt(currentRoom.room_number.substring(0, 2)).toString()][key] =
          (linensNeeded.value[parseInt(currentRoom.room_number.substring(0, 2)).toString()][key] ||
            0) + linens_for_checkOut[currentRoom.room_type][key]
      })
    }
  })
  console.log(linensNeeded.value)
}

function changeStatus(room, newStatus) {
  hotelData.value.changeStatus(room, newStatus)
}
</script>

<template>
  <div class="app-class">
    <div v-for="room in hotelData.rooms" :key="room.room_number">
      <RoomComponent :room-obj="room" @change-status="changeStatus" />
    </div>
    <button @click="calculateForFloors">DO IT!</button>
  </div>

  <vTable :table-obj="linensNeeded" />
</template>

<style scoped>
.app-class {
  min-width: 400px;
  width: 100%;
}
</style>
