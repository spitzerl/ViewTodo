<template>
    <v-container>
        <!-- Formulaire pour ajouter un élément à la liste -->
        <v-form @submit.prevent="addTodo" class="mt-10">
            <v-row>
                <v-col cols="10">
                    <v-text-field v-model="newTodo" required placeholder="Nouvelle tâche" label="Nouvelle tâche" />
                </v-col>
                <v-col cols="2">
                    <v-btn block prepend-icon="$plus" color="primary" @click="addTodo"> Ajouter </v-btn>
                </v-col>
            </v-row>
        </v-form>
        <!-- Liste des todo -->
        <v-list class="bg-transparent">
            <v-list-item v-for="todo in todos" :key="todo.id" class="bg-transparent">
                <v-card class="w-100 rounded-lg bg-primary">
                    <v-card-text class="d-flex justify-space-between align-center">
                        <!-- Titre-->
                        <v-list-item-title>{{ todo.text }}</v-list-item-title>
                        <!-- Bouton delete -->
                        <v-btn icon @click="removeTodo(todo)">
                            <v-icon>mdi-delete</v-icon>
                        </v-btn>
                    </v-card-text>
                </v-card>
            </v-list-item>
        </v-list>
    </v-container>
</template>

<script setup>
    import { ref, watchEffect } from 'vue'

    // Donne à chaque todo un id unique
    let id = 0

    const newTodo = ref('')
    const todos = ref([])

    // On charge les todos depuis le cache du navigateur
    const savedTodos = localStorage.getItem('todos')
    // Si on trouve des todos dans le cache, on les charge
    if (savedTodos) {
        todos.value = JSON.parse(savedTodos)
        // Mettre à jour l'id pour qu'il continue à partir du dernier id utilisé
        id = todos.value.length > 0 ? todos.value[todos.value.length - 1].id + 1 : 0
    }
    // Sinon, on initialise les todos avec des valeurs par défaut
    else {
        todos.value = [
            { id: id++, text: 'Apprendre le HTML' },
            { id: id++, text: 'Apprendre le JavaScript' },
            { id: id++, text: 'Apprendre Vue' },
        ]
    }

    // On sauvegarde les todos dans le cache du navigateur à chaque modification
    watchEffect(() => {
        localStorage.setItem('todos', JSON.stringify(todos.value))
    })

    // Fonction pour ajouter un todo
    function addTodo() {
        if (newTodo.value.trim() !== '') {
            todos.value.push({ id: id++, text: newTodo.value })
            newTodo.value = ''
        }
    }

    // Fonction pour supprimer un todo
    function removeTodo(todo) {
        todos.value = todos.value.filter((t) => t.id !== todo.id)
    }
</script>

<style>
    /* Ajouter des styles si nécessaire */
</style>
