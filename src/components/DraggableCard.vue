<template>
  <div @click="openEditor">
    <v-card class="kanban-card" elevation="2" tile outlined>
      {{ element.name }}
      <div class="card-right">
        <v-avatar color="indigo" size="24">
          <span class="white--text">AB</span>
        </v-avatar>
        <v-avatar color="orange" size="24" style="margin-left: -10px">
          <span class="white--text">CD</span>
        </v-avatar>
        <span class="avater-ellipsis">...</span>
      </div>
    </v-card>
    <CardEditor
      v-if="isOpenEditor"
      :element="element"
      :isOpenEditor="isOpenEditor"
      @closeDialog="closeDialog"
    />
  </div>
</template>

<script>
import Vue from 'vue';
import CardEditor from "@/components/CardEditor";
// import { User } from "../types/User";
export default Vue.extend({
  name: "DraggableCard",
  components: {
    CardEditor
  },
  props: {
    element: {}
  },
  data() {
    return {
      statusChip: {},
      isOpenEditor: false,
      assignee: "",
      notStartBgColor: "#f5f5f5",
      inProgressBgColor: "#afeeee",
      lateProgressBgColor: "#f08080"
    }
  },
  methods: {
    openEditor() {
      this.isOpenEditor = !this.isOpenEditor;
    },
    closeDialog() {
      this.isOpenEditor = !this.isOpenEditor;
    }
  }
})
</script>

<style lang="scss" scoped>
.kanban-card {
  padding: 4px;
  cursor: pointer;
  .card-right {
    display: initial;
    position: absolute;
    right: 8px;
    .avater-ellipsis {
      vertical-align: sub;
    }
  }
}
.kanban-card:hover {
  background-color: #dbedff;
}
</style>