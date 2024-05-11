<script setup>
import RoomComponent from './components/RoomComponent.vue'
import { ref } from 'vue';

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

function changeStatus(room, newStatus) {
  hotelData.value.changeStatus(room, newStatus)
}

</script>

<template>
  <div class="app">
    <div v-for="room in hotelData.rooms" :key="room.room_number">
      <RoomComponent
        :room-obj="room"
        @change-status="changeStatus"
      />
    </div>
    <button @click="console.log(hotelData.rooms)">Show console</button>
  </div>
</template>

<style scoped></style>
