<script setup>
import { ref } from 'vue'
import RoomComponent from './components/RoomComponent.vue'
import vTable from './components/vTable.vue'
import parseString from './components/parseString.vue'

import { linens_for_checkOut, linens_for_stayOver } from './components/linens_for_rooms'
import { rooms_info } from './components/rooms_info'

let showRoomList = ref(true)
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
  12: { floor: '12' },
  13: { floor: 'Total' }
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
    12: { floor: '12' },
    13: { floor: 'Total' }
  }
  hotelData.value.rooms.forEach((currentRoom) => {
    const floorNumber = parseInt(currentRoom.room_number.substring(0, 2)).toString()

    // add linens if room has 'stay over' status
    if (currentRoom.status === 'Stay Over') {
      Object.keys(linens_for_stayOver[currentRoom.room_type]).forEach((key) => {
        linensNeeded.value[floorNumber][key] =
          (linensNeeded.value[floorNumber][key] || 0) +
          linens_for_stayOver[currentRoom.room_type][key]

        // Total number of particular type of linens
        linensNeeded.value["13"][key] =
          (linensNeeded.value["13"][key] || 0) +
          linens_for_stayOver[currentRoom.room_type][key]
      })

      // add linens if room has 'check out' status
    } else if (currentRoom.status === 'Check Out') {
      const floorNumber = parseInt(currentRoom.room_number.substring(0, 2)).toString()
      Object.keys(linens_for_checkOut[currentRoom.room_type]).forEach((key) => {
        linensNeeded.value[floorNumber][key] =
          (linensNeeded.value[floorNumber][key] || 0) +
          linens_for_checkOut[currentRoom.room_type][key]

        // Total number of particular type of linens
        linensNeeded.value["13"][key] =
          (linensNeeded.value["13"][key] || 0) +
          linens_for_checkOut[currentRoom.room_type][key]
      })
      // count total number of checkouts for each floor
      linensNeeded.value[floorNumber]['totalCheckOuts'] =
        linensNeeded.value[floorNumber]['totalCheckOuts'] != undefined 
          ? linensNeeded.value[floorNumber]['totalCheckOuts'] + 1
          : 1
      // count total number of checkouts for all floors
      linensNeeded.value["13"]['totalCheckOuts'] =
        linensNeeded.value["13"]['totalCheckOuts'] != undefined 
          ? linensNeeded.value["13"]['totalCheckOuts'] + 1
          : 1
    }
  })
  console.log(linensNeeded.value)
}

function changeStatus(room, newStatus) {
  console.info(room, newStatus)
  // update room status
  hotelData.value.changeStatus(room, newStatus)

  calculateForFloors()
}

const hideRoomsList = () => {
  // hide list of rooms
  showRoomList.value = !showRoomList.value
}
</script>

<template>
  <parseString @change-status="changeStatus"></parseString>

  <div class="app-class" v-show="showRoomList">
    <div v-for="room in hotelData.rooms" :key="room.room_number">
      <RoomComponent :room-obj="room" @change-status="changeStatus" />
    </div>
  </div>

  <div class="btns">
    <button @click="calculateForFloors">DO IT!</button>
    <button @click="hideRoomsList">Hide/show rooms</button>
  </div>
  <vTable :table-obj="linensNeeded" />
</template>

<style scoped>
.app-class,
.btns {
  min-width: 400px;
  width: 100%;
}

.btns {
  display: flex;
  justify-content: space-around;
  margin: 10px;
}

.btns button {
  height: 40px;
  width: 30%;
}
</style>
