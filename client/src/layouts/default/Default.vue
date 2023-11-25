<template>
  <v-app
    style="
       {
        background: rgb(2, 0, 36);
        background: linear-gradient(
          311deg,
          rgba(2, 0, 36, 1) 0%,
          rgba(53, 192, 101, 1) 100%
        );
      }
    "
  >
    <default-bar />

    <default-view />
  </v-app>
</template>

<script setup>
import DefaultBar from "./AppBar.vue";
import DefaultView from "./View.vue";
</script>
