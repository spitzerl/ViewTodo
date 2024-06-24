<template>
    <v-app :theme="theme">
        <v-main>
            <Navbar :theme="theme" @toggle-theme="theme = theme === 'light' ? 'dark' : 'light'" />
            <ToDo />
        </v-main>
    </v-app>
</template>

<script setup>
    import { ref } from 'vue'

    const theme = ref('light')
</script>
