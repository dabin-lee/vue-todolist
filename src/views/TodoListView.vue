<template>
  <div>
    <p>할일 {{ countSum }}개 남음</p>
    <ListItem
      v-for="(item, index) in todoItems"
      :key="item.id"
      :item="item"
      :index="index"
      @deleteItem="deleteItem"
      @checked="completed"
    />
    <button @click="allClear">전체삭제</button>

    <div class="input-group mb-3 mt-4">
      <input
        type="text"
        class="form-control"
        v-model="itemValue"
        v-on:keyup.enter="addItem"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
        @click="addItem"
      >
        add
      </button>
    </div>
  </div>
</template>

<script>
import ListItem from "./todolist/ListItem.vue";
export default {
  components: { ListItem },
  data() {
    return {
      todoItems: [],
      itemValue: "",
      count: 0,
    };
  },
  methods: {
    addItem() {
      if (this.itemValue !== "") {
        const value = {
          id: Math.random(),
          content: this.itemValue,
          checked: false,
        };
        localStorage.setItem(this.itemValue, JSON.stringify(value));
        this.itemValue = "";
        this.newItem();
      }
    },
    deleteItem(item, index) {
      localStorage.removeItem(item.content);
      this.todoItems.splice(index, 1);
    },
    allClear() {
      localStorage.clear();
    },
    newItem() {
      if (localStorage.length > 0) {
        const newList = [];

        for (let i = 0; i < localStorage.length; i++) {
          const item = JSON.parse(localStorage.getItem(localStorage.key(i)));
          newList.push(item);
        }

        this.todoItems = newList;
      }
    },
  },
  mounted() {
    this.newItem();
  },
  // watch: {
  //   completed: {
  //     handler: function (value) {
  //       console.log("value: ", value);
  //     },
  //   },
  // },
  computed: {
    countSum() {
      const checked = this.todoItems.filter((item) => item.checked === true);
      return checked.length;
    },
  },
};
</script>

<!-- 
watch  데이터 값이바뀌었을 때 
computed 
-->
