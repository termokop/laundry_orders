<script setup>
import { ref } from 'vue';
// import { sample } from './string_template';

const emit = defineEmits(['changeStatus'])

let strForParse = ref('')

const parseTheString = (() => {
    let strWithoutSpaces = strForParse.value.replace(/\n/g, "").replace(/\s+/g, "")

    const regex = /(\d{4})([A-Za-z]+)/g;

    const result = []

    let match;
    while ((match = regex.exec(strWithoutSpaces)) !== null) {
        // Push matched groups into the result array
        result.push([match[1], match[2]]);
    }
    console.log(result)
    changeStatusForArr(result)
})

const changeStatusForArr = (arr => {
    for (let i = 0; i < arr.length; i++) {
        if(arr[i][1] == "Stayover") {
            emit('changeStatus',arr[i][0], 'Stay Over')
        } else {
            emit('changeStatus',arr[i][0], 'Check Out')
        }
        
    }
})



// for (let i = 0; i < arr.length; i++) {
//     if(arr[i] == '') {
//         arr.splice([i], 1)
//     }
// }


</script>


<template>

    <div>
        <textarea name="strForParse" id="" cols="100" rows="10" v-model="strForParse"></textarea>
        <div class="btns">
            <button @click="parseTheString">Parse the text</button>
        </div>
    </div>
</template>

<style scoped>

textarea {
    width: 100%;
}

</style>