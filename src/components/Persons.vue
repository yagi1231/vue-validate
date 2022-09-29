<script setup lang="ts">
import PersonPostForm from './PersonPostForm.vue';
import PersonList from './PersonList.vue';
import { ref, Ref } from 'vue';
    
    export type Person  = {
        id: number,
        name: string,
        age: number
    }
    
    
    const persons: Ref<Person[]> =  ref([{id: 0, name: 'john', age: 26}, {id: 1, name: 'name', age: 24}])


const registerPerson = (person: Person) => {
    persons.value.push(person)
}

const deleteButton = (id: number) => {
    persons.value = persons.value.filter(p => p.id !== id)
}


</script>

<template>
    <div class="container">
        <h1></h1>
        <PersonPostForm @register="registerPerson"/>
        <div class="list-container">
            <ul>
                <PersonList 
                :persons="persons"
                @delete="deleteButton"
                />
            </ul>
        </div>
    </div>
</template>

<style scoped>
    .container {
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>