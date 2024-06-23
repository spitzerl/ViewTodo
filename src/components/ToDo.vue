<template>
    <v-container>
        <!-- Formulaire pour ajouter un élément à la liste -->
        <v-form @submit.prevent="addTodo">
            <v-row>
                <v-col cols="9">
                    <v-text-field v-model="newTodo" required placeholder="Nouvelle tâche" label="Nouvelle tâche" />
                </v-col>
                <v-col cols="3">
                    <v-btn color="primary" @click="addTodo">Ajouter une tâche</v-btn>
                </v-col>
            </v-row>
        </v-form>
        <!-- Liste des todo -->
        <v-list>
            <v-list-item v-for="todo in todos" :key="todo.id" class="d-flex mb-6 bg-surface-variant">
                <v-list-item-content class="ma-2 pa-2 me-auto">
                    <v-list-item-title>{{ todo.text }}</v-list-item-title>
                </v-list-item-content>
                <v-list-item-action class="ma-2 pa-2">
                    <v-btn icon @click="removeTodo(todo)">
                        <v-icon>mdi-delete</v-icon>
                    </v-btn>
                </v-list-item-action>
            </v-list-item>
        </v-list>
    </v-container>
</template>

<script setup>
    import { ref } from 'vue'

    // donne à chaque todo un id unique
    let id = 0

    const newTodo = ref('')
    const todos = ref([
        { id: id++, text: 'Apprendre le HTML' },
        { id: id++, text: 'Apprendre le JavaScript' },
        { id: id++, text: 'Apprendre Vue' },
    ])

    function addTodo() {
        todos.value.push({ id: id++, text: newTodo.value })
        newTodo.value = ''
    }

    function removeTodo(todo) {
        todos.value = todos.value.filter((t) => t !== todo)
    }
</script>

<style>
    /* Ajouter des styles si nécessaire */
</style>
