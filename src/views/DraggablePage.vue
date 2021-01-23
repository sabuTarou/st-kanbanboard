<template>
  <div class="draggablePage">
    <Draggable
      :lists="lists"
      :isDeleteList="true"
      :isAddList="true"
      @addList="addList"
      @deleteList="deleteList"
      @onChange="onchange"
      @addCard="addCard"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import Draggable from '@/components/Draggable'

export default {
  name: 'DraggablePage',
  components: {
    Draggable
  },
  data() {
    return {
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
      }],
    }
  },
  methods: {
    onchange(e, key) {
      console.log("onChange", e, key);
    },
    addList(title) {
      console.log("addList", title);
    },
    deleteList(key) {
      console.log("deleteList", key);
    },
    addCard(key, cardObj) {
      console.log("addCard", key, cardObj);
    }
  }
}
</script>
