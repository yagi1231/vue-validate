<script setup lang="ts">
import { Person } from './Persons.vue';

    type Props = {
        persons: Person[]
    }

    defineProps<Props>()
const emit = defineEmits(['delete'])
const deletePerson = (id: number, name: string) => {
if(confirm(name + "を消しますか？")) {
    emit('delete', id)
}
}

</script>

<template>
    <li v-for="person in persons" :key="person.id" class="person-list">
    <span>{{ person.name }}</span>
    <span>{{ person.age }}</span>
    <button @click="deletePerson(person.id, person.name)">delete</button>
</li>
</template>

<style scoped>
    .person-list {
        list-style: none;
        margin-bottom: 12px;
        border-radius: 4px;
        font-size: 20px;
        display: flex;
        justify-content: space-between;
        background-color: rgb(228, 201, 103);
        width:300px;
        padding: 8px 20px;
    }
</style>