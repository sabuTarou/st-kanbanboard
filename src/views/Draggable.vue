<template>
  <div class="draggable-list ml-2 pt-2 pb-2">
    <div class="kanban-list mr-4" v-for="(list, key) in lists" :key="key">
      <div class="title group-title">
        {{ list.title }}({{ list.tasks.length }})
        <span><v-icon @click="deleteList(key)">mdi-delete</v-icon></span>
      </div>
      <draggable
        class="list-group pt-2 pr-2 pl-2"
        :list="list.tasks"
        group="kanban"
        draggable=".item"
        v-bind="dragOptions"
        @start="drag = true"
        @end="drag = false"
        @change="log"
      >
        <div slot="footer">
          <v-btn class="mt-2" text secondary @click="add(list.tasks)"
            >カードを追加する</v-btn
          >
        </div>
        <draggableCard
          class="list-group-item item"
          v-for="(element, index) in list.tasks"
          :element="element"
          :key="index"
        >
        </draggableCard>
      </draggable>
    </div>
    <v-btn class="add-kanban-list mr-4" outlined @click="addNewList">
      リストを追加する
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
  data() {
    return {
      drag: false,
      lists: [{
        title: "自分", tasks: [
          { name: "John", id: 1, right: [{ name: "AB", color: "indigo" }, { name: "CD", color: "orange" }] },
          { name: "Joao", id: 2, right: [] },
          { name: "Jean", id: 3, right: [{ name: "AB", color: "indigo" }, { name: "CD", color: "orange" }, { name: "EF", color: "green" }] },
          { name: "Gerard", id: 4, right: [{ name: "AB", color: "indigo" }, { name: "CD", color: "orange" }, { name: "EF", color: "green" }, { name: "GH", color: "#808000" }] }
        ]
      }, {
        title: "Aさん", tasks: [
          { name: "Juan", id: 5, right: [] },
          { name: "Edgard", id: 6, right: [] },
          { name: "Johnson", id: 7, right: [] }
        ]
      }, {
        title: "Bさん", tasks: [
          { name: "Taro", id: 8, right: [] },
          { name: "Jiro", id: 9, right: [] },
          { name: "Saburo", id: 10, right: [] },
          { name: "Shiro", id: 11, right: [] }
        ]
      }]
    };
  },
  methods: {
    add: function(list) {
      const id = Math.floor(Math.random() * (500 - 100) + 100);
      list.push({ name: "Issue" + id, id });
    },
    log: function() {
    },
    addNewList() {
      this.lists.push({ title: "New List", tasks: [] });
    },
    deleteList(key) {
      this.lists.splice(key, 1);
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