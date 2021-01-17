<template>
  <v-dialog v-model="isOpenEditor" scrollable persistent max-width="400px">
    <v-card>
      <v-card-title>{{ element.name }}</v-card-title>
      <v-divider></v-divider>
      <v-card-text style="height: 300px"> {{ element }} </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>
        <v-btn color="blue darken-1" text @click="closeDialog"> Cansel </v-btn>
        <v-btn color="blue darken-1" text @click="closeDialog"> Save </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
export default {
  name: "CardEditor",
  props: {
    isOpenEditor: {
      type: Boolean,
      default: false
    },
    element: {
      type: Object
    }
  },
  data() {
    return {
      dialogm1: ''
    }
  },
  methods: {
    closeDialog() {
      this.$emit("closeDialog");
    }
  },
}
</script>
