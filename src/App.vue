<script setup>
import RoomComponent from './components/RoomComponent.vue'

import vTable from './components/vTable.vue';
import { ref } from 'vue';

import {linens_for_checkOut, linens_for_stayOver} from './components/linens_for_rooms'

let linensNeeded = ref({
  "03": {floor: "03"},
  "04": {floor: "04"},
  "05": {floor: "05"},
  "06": {floor: "06"},
  "07": {floor: "07"},
  "08": {floor: "08"},
  "09": {floor: "09"},
  "10": {floor: "10"},
  "11": {floor: "11"},
  "12": {floor: "12"},
})

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


const calculateForFloors = (() => {
  linensNeeded.value = {
  "03": {floor: "03"},
  "04": {floor: "04"},
  "05": {floor: "05"},
  "06": {floor: "06"},
  "07": {floor: "07"},
  "08": {floor: "08"},
  "09": {floor: "09"},
  "10": {floor: "10"},
  "11": {floor: "11"},
  "12": {floor: "12"},
}
  hotelData.value.rooms.forEach(currentRoom => {
    if(currentRoom.status === "Stay Over") {
      Object.keys(linens_for_stayOver[currentRoom.room_type]).forEach(key => {
        linensNeeded.value[currentRoom.room_number.substring(0,2)][key] = (linensNeeded.value[currentRoom.room_number.substring(0,2)][key] || 0) + linens_for_stayOver[currentRoom.room_type][key]
      })
    } else if(currentRoom.status === "Check Out") {
      Object.keys(linens_for_checkOut[currentRoom.room_type]).forEach(key => {
        linensNeeded.value[currentRoom.room_number.substring(0,2)][key] = (linensNeeded.value[currentRoom.room_number.substring(0,2)][key] || 0) + linens_for_checkOut[currentRoom.room_type][key]
      })
    }
  })
  console.log(linensNeeded.value)
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
    <button @click="calculateForFloors">DO IT!</button>
  </div>

  <vTable :table-obj="linensNeeded"/>
  
</template>

<style scoped>

.app-class {
  min-width: 400px;
  width: 100%;
}

</style>
