<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { ref } from 'vue'

const inputingName = ref<string>('')
const inputingAge = ref<number>(0)

const emit = defineEmits(['register'])

const register = () => {
    const person = { id: Math.random(), name: inputingName.value, age: inputingAge.value }
    console.log(person)
    emit('register', person)
}

const nameLength = 15

const isValidName = computed(()=> {
    if(inputingName.value.length >= nameLength) {
        return false
    }else {
        return true
    }
})
const color = computed(() => {
    return isValidName.value ? 'white' : 'red'
})

</script>

<template>
    <div class="person-container">
        <div class="input-container">
            <div class="input-column">
            <span>name:</span>
            <input class="input-name" v-model="inputingName"/>
        </div>
        <span v-if="!isValidName">{{ nameLength }}以内で</span>
        </div>
        <div class="input-container">
            <div class="input-column">
            <span>age:</span>
            <input class="input-age"  v-model="inputingAge" type="number"/>
        </div>
        </div>
        <button :disabled="!isValidName" class="register" @click="register">register</button>
    </div>
</template>

<style scoped>
    .input-column  {
        width:200px;
        display: flex;
        justify-content: space-between;
    }
    .person-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: rgb(255,241,226);
        padding: 24px 0;
        width: 50%;
        margin-bottom: 12px;
        border-radius: 4px;
    }

    span {
        font-size: 20px;
        font-weight: bold;
    }

    input {
        width:120px;
        margin-bottom: 20px;
    }

    .input-containe {
        display: flex;
        flex-direction: column;
        justify-content: center;
        height: 50px;
        margin-bottom: 20px;
    }

    .input-name {
        background-color: v-bind(color);
    }
</style>