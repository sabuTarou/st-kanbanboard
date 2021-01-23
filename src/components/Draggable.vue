<template>
  <div class="draggable-list ml-2 pt-2 pb-2">
    <div class="kanban-list mr-4" v-for="(list, key) in lists" :key="key">
      <div class="title group-title">
        {{ list.title }}({{ list.tasks.length }})
        <span
          ><v-icon v-if="isDeleteList" @click="deleteList(key)"
            >mdi-delete</v-icon
          ></span
        >
      </div>
      <draggable
        class="list-group pt-2 pr-2 pl-2"
        :list="list.tasks"
        group="kanban"
        draggable=".item"
        v-bind="dragOptions"
        @start="drag = true"
        @end="drag = false"
        @change="onChange($event, key)"
      >
        <div slot="footer">
          <v-btn
            class="mt-2"
            :class="'show-add-input-btn-' + key"
            v-if="showAddCardBtn[key]"
            text
            secondary
            @click="showCardInput(key)"
            >Add Card</v-btn
          >
          <v-btn
            class="mt-2"
            :class="'add-card-btn-' + key"
            color="success"
            secondary
            v-if="!showAddCardBtn[key]"
            @click="addCard(list.tasks, key)"
            >Add Card</v-btn
          >
        </div>
        <draggableCard
          class="list-group-item item"
          v-for="(element, index) in list.tasks"
          :element="element"
          :key="index"
        >
        </draggableCard>
        <v-text-field
          :class="'add-card-field-' + key"
          class="mt-1"
          background-color="white"
          v-if="!showAddCardBtn[key]"
          @change="changeTitleField($event, key)"
        />
      </draggable>
    </div>
    <v-btn class="add-kanban-list mr-4" outlined @click="addNewList">
      Add List
    </v-btn>
  </div>
</template>
<script>
import draggable from "vuedraggable";
import draggableCard from "@/components/DraggableCard";

export default {
  name: "Draggable",
  components: {
    draggable,
    draggableCard
  },
  props: {
    lists: {
      type: Array,
      default: function() {
        return [];
      }
    },
    isDeleteList: {
      type: Boolean,
      default: false
    },
    isAddList: {
      type: Boolean,
      default: false
    },
  },
  data() {
    return {
      drag: false,
      newTitle: [],
      showAddCardBtn: []
    };
  },
  methods: {
    showCardInput(key) {
      this.$set(this.showAddCardBtn, [key], false);
    },
    addCard(list, key) {
      const id = Math.floor(Math.random() * (500 - 100) + 100);
      const cardObj = { name: this.newTitle[key], id, right: [] };
      list.push(cardObj);
      this.newTitle[key] = "";
      this.$set(this.showAddCardBtn, [key], true);
      this.$emit("addCard", key, cardObj);
    },
    changeTitleField(e, key) {
      this.newTitle[key] = e;
    },
    onChange(e, key) {
      this.$emit("onChange", e, key);
    },
    addNewList() {
      const listTitle = "New List";
      this.lists.push({ title: listTitle, tasks: [] });
      this.showAddCardBtnConstructor();
      this.$emit("addList", listTitle);
    },
    deleteList(key) {
      this.lists.splice(key, 1);
      this.$emit("deleteList", key);
    },
    showAddCardBtnConstructor() {
      for (let i = 0; i < this.lists.length; i++) {
        this.showAddCardBtn[i] = true;
      }
    }
  },
  computed: {
    dragOptions() {
      return {
        animation: 200,
        group: "myGroup",
        disabled: false,
        ghostClass: "ghost"
      };
    }
  },
  created() {
    this.showAddCardBtnConstructor();
  }
};
</script>
<style lang="scss" scoped>
.draggable-list {
  height: 100%;
  display: flex;
  flex-wrap: nowrap;
  overflow-x: auto;
  .kanban-list {
    // height: 100%;
    min-width: 300px;
    white-space: nowrap;
    .group-title {
      min-height: 32px;
      max-height: 32px;
    }
    .list-group {
      box-sizing: border-box;
      // height: 100%;
      border: gray solid 1px;
    }
  }
}
.add-kanban-list {
  width: 300px;
  margin-top: 32px;
  min-width: 300px;
}
.flip-list-move {
  transition: transform 0.5s;
}
.no-move {
  transition: transform 0s;
}
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.list-group {
  min-height: 60px;
}
.list-group-item {
  cursor: move;
}
</style>