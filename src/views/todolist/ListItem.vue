<template>
  <ul class="list-group">
    <li class="d-flex justify-content-between">
      <div class="d-flex align-items-center">
        <input
          type="checkbox"
          :checked="item.checked"
          v-on:change="checked(item)"
        />
        <p :class="item.checked ? 'finishItem' : null">
          {{ item.content }}
        </p>
      </div>
      <button :class="btnX" @click="deleteItem">x</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "todo-list-item",
  props: {
    item: Object,
    index: Number,
  },
  data() {
    return {
      btnX: {
        border: "none",
      },
      // completed: false,
    };
  },
  methods: {
    deleteItem() {
      this.$emit("deleteItem", this.item, this.index);
    },
    checked(item) {
      // this.completed = !this.completed;
      item.checked = !item.checked;
      localStorage.setItem(item.content, JSON.stringify(item));
    },
  },
  // watch: {
  //   checked: {
  //     handler: function (newState) {
  //       this.$emit("completed", newState);
  //     },
  //   },
  // },
};
</script>

<style>
.finishItem {
  /* color: red; */
  text-decoration: line-through;
  text-decoration-color: red;
  color: rgb(206, 212, 218);
}
.defaultItem {
  color: blue;
}
</style>
