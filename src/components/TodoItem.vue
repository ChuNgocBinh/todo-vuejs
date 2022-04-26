<template>
  <div class="totoContainer">
    <input type="checkbox" :checked="data.completed" @change="onChange" />
    <div :class="['totoContent', data.completed ? 'todoComplete' :'' ]">{{ data.title }}</div>
    <button @click="onDelete">Delete</button>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "TodoItem",
  props: ["data"],

  setup(props, context) {
    console.log(props);
    console.log("context:", context);
    const todoChecked = ref("");
    console.log(todoChecked);

    const onChange = () => {
      context.emit("onChecked",props.data.id);
    };

    const onDelete = () => {
      context.emit("onDeleteItem", props.data.id);
    };

    return { todoChecked, onChange, onDelete };
  },
};
</script>

<style scoped>
.totoContainer {
  display: flex;
  padding: 10px 20px;
  align-items: center;
  background-color: #ccc;
  margin: 10px 20px;
  border-radius: 10px;
}



.totoContent {
  flex-grow: 1;
  padding: 0 20px;
}

.todoComplete{
  text-decoration: line-through;
}
</style>