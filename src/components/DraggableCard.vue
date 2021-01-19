<template>
  <div @click="openEditor">
    <v-card class="kanban-card" elevation="2" tile outlined>
      {{ element.name }}
      <div class="card-right">
        <v-avatar
          class="avater"
          :color="item.color"
          size="24"
          v-for="(item, key) in topThree"
          :key="key"
        >
          <span class="white--text">{{ item.name }}</span>
        </v-avatar>
        <span class="avater-ellipsis" v-if="element.right.length > 3">...</span>
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
      isOpenEditor: false
    }
  },
  methods: {
    openEditor() {
      this.isOpenEditor = !this.isOpenEditor;
    },
    closeDialog() {
      this.isOpenEditor = !this.isOpenEditor;
    }
  },
  computed: {
    topThree() {
      return this.element.right === undefined ? [] : this.element.right.slice(0, 3);
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
    .avater {
      margin-left: -12px;
    }
    .avater-ellipsis {
      vertical-align: sub;
    }
  }
}
.kanban-card:hover {
  background-color: #dbedff;
}
</style>