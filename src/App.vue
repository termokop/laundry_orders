<script setup>
import RoomComponent from './components/RoomComponent.vue'
import { ref } from 'vue';

import {linens_for_checkOut, linens_for_stayOver} from './components/linens_for_rooms'


const linensNeeded = {
  "03": {},
  "04": {},
  "05": {},
  "06": {},
  "07": {},
  "08": {},
  "09": {},
  "10": {},
  "11": {},
  "12": {},
  
}

const hotelData = ref({
    rooms: [
        {
            room_number: "0302",
            room_type: "CK",
            status: "None"
        },    {
            room_number: "0303",
            room_type: "CK",
            status: "None"
        },    {
            room_number: "0304",
            room_type: "CQ",
            status: "None"
        },    {
            room_number: "0305",
            room_type: "CQ",
            status: "None"
        },    {
            room_number: "0306",
            room_type: "CQ",
            status: "None"
        },    {
            room_number: "0307",
            room_type: "CQQ",
            status: "None"
        },    {
            room_number: "0401",
            room_type: "CQQ",
            status: "None"
        },    {
            room_number: "0402",
            room_type: "CK",
            status: "None"
        },    {
            room_number: "0403",
            room_type: "CQ",
            status: "None"
        },    {
            room_number: "0501",
            room_type: "CK",
            status: "None"
        },    {
            room_number: "0502",
            room_type: "CQ",
            status: "None"
        },
       
    ],
    changeStatus(room, newStatus) {
        for (let i = 0; i < this.rooms.length; i++) {
            if(this.rooms[i].room_number == room) {
                this.rooms[i].status = newStatus
                break
            }
        }
    }
})

// 
// function createTheTable() {
//   let floorNumber = 3
//   let objFloor = {}
//   for (let i = 0; i < hotelData.value.rooms.length; i++) {
//     const currentRoom = hotelData.value.rooms[i]

//     if(currentRoom.room_number.substring(0,2) == floorNumber) {
      
//       objFloor.floor = floorNumber
//       if(currentRoom.status == "Check Out") {
        
//         Object.keys(linens_for_checkOut[currentRoom.room_type]).forEach(key => {
//           objFloor[key] = (objFloor[key] || 0) + linens_for_checkOut[currentRoom.room_type][key]
//         })
//         console.log(objFloor)
//       }

//       if(currentRoom.status == "Stay Over") {
//         Object.keys(linens_for_stayOver[currentRoom.room_type]).forEach(key => {
//           objFloor[key] = (objFloor[key] || 0) + linens_for_stayOver[currentRoom.room_type][key]
//         })
//       }
//     }
//     if(currentRoom.room_number.substring(2,2) == 15) {
//       floorNumber++
//       linensNeeded.push(objFloor)
//       objFloor = {}
//     }
    
//   }

//   console.log(linensNeeded)
// }

const createTheTable = (() => {
  hotelData.value.rooms.forEach(currentRoom => {
    if(currentRoom.status === "Stay Over") {
      Object.keys(linens_for_stayOver[currentRoom.room_type]).forEach(key => {
        linensNeeded[currentRoom.room_number.substring(0,2)][key] = (linensNeeded[currentRoom.room_number.substring(0,2)][key] || 0) + linens_for_stayOver[currentRoom.room_type][key]
      })
    } else if(currentRoom.status === "Check Out") {
      Object.keys(linens_for_checkOut[currentRoom.room_type]).forEach(key => {
        linensNeeded[currentRoom.room_number.substring(0,2)][key] = (linensNeeded[currentRoom.room_number.substring(0,2)][key] || 0) + linens_for_checkOut[currentRoom.room_type][key]
      })
    }
  })
  console.log(linensNeeded)
})

function changeStatus(room, newStatus) {
  hotelData.value.changeStatus(room, newStatus)
}

</script>

<template>
  <div class="app-class">
    <div v-for="room in hotelData.rooms" :key="room.room_number">
      <RoomComponent
        :room-obj="room"
        @change-status="changeStatus"
      />
    </div>
    <button @click="createTheTable">DO IT!</button>
  </div>
</template>

<style scoped>

.app-class {
  min-width: 400px;
  width: 100%;
}

</style>
