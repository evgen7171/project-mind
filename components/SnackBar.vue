<template>
  <v-snackbar v-model="snackbar">
    {{ text }}

    <v-btn color="pink" text @click="snackbar = false"> Close </v-btn>
  </v-snackbar>
</template>

<script>
export default {
  name: 'Snakbar',
  data() {
    return {
      text: '001100 hello ...',
      snakbar: false,
    }
  },
}
</script>

<style scoped></style>
