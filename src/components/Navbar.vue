<template>
    <v-app-bar :elevation="14" class="px-2">
        <template v-slot:prepend>
            <v-app-bar-nav-icon></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title>View Todo</v-app-bar-title>

        <template v-slot:append>
            <v-btn :icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'" @click="onClick"></v-btn>
        </template>
    </v-app-bar>
</template>

<script setup>
    defineProps(['theme'])
    const emit = defineEmits(['toggle-theme'])

    function onClick() {
        emit('toggle-theme')
    }
</script>
