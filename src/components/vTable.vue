<script setup>
defineProps({
  tableObj: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <div>
    <table>
      <tr>
        <th>Floor</th>
        <th>K pillow sham</th>
        <th>Q pillow sham</th>
        <th>K pillow case</th>
        <th>Q pillow case</th>
        <th>K sheet</th>
        <th>Q sheet</th>
        <th>K Duvet</th>
        <th>Q Duvet</th>
        <th>Bath matt</th>
        <th>Face cloth</th>
        <th>Bath Robe</th>
        <th>Hand towel</th>
        <th>Bath towel</th>
      </tr>
      <tr v-for="floor in tableObj" :key="floor.floor">
        <td>{{floor.floor}}</td>
        <td>{{ Math.ceil(floor.king_pillow_sham) || 0 }}</td>
        <td>{{ Math.ceil(floor.queen_pillow_sham) || 0 }}</td>
        <td>{{ Math.ceil(floor.king_pillow_case) || 0 }}</td>
        <td>{{ Math.ceil(floor.queen_pillow_case) || 0 }}</td>
        <td>{{ Math.ceil(floor.king_sheet) || 0 }}</td>
        <td>{{ Math.ceil(floor.queen_sheet) || 0 }}</td>
        <td>{{ Math.ceil(floor.king_duvet_cover) || 0 }}</td>
        <td>{{ Math.ceil(floor.queen_duvet_cover) || 0 }}</td>
        <td>{{ Math.ceil(floor.bath_matt) || 0 }}</td>
        <td>{{ Math.ceil(floor.face_cloth) || 0 }}</td>
        <td>{{ Math.ceil(floor.bath_robe) || 0 }}</td>
        <td>{{ Math.ceil(floor.hand_towel) || 0 }}</td>
        <td>{{ Math.ceil(floor.bath_towel) || 0 }}</td>
      </tr>
    </table>
  </div>
</template>
