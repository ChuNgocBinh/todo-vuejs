
<template>
  <div class="container">
    <div class="header">Todo list</div>
    <CreateTodo @onClickCreate="createTodo"/>
    <TodoItem
      v-for="item in todos"
      :key="item.id"
      :data="item"
      @onChecked="onChecked"
      @onDeleteItem="onDeleteTodoItem"
    />
  </div>
</template>

<script>
import { onMounted, ref } from "@vue/runtime-core";
import TodoItem from "./components/TodoItem.vue";
import CreateTodo from './components/CreateTodo.vue';

export default {
  name: "App",
  components: {
    TodoItem,
    CreateTodo
  },

  setup() {
    const checkedName = ref([]);
    const todos =ref([
      {
        id: 1,
        title: "delectus aut autem",
        completed: false
      },
      {
        id: 2,
        title: "quis ut nam facilis et officia qui",
        completed: false
      },
      {
        id: 3,
        title: "fugiat veniam minus",
        completed: false
      },
      {
        id: 4,
        title: "et porro tempora",
        completed: true
      },
      {
        id: 5,
        title: "laboriosam mollitia et enim quasi adipisci quia provident illum",
        completed: false
      },
    ])

    onMounted(() => {
  
        checkedName.value = todos.value.filter(item=> item.completed===true)
    });

    const onChecked = (id) => {
      todos.value=todos.value.map(item=>{
        if(item.id===id){
          item.completed=!item.completed
        }
        return item
      })
    };

    const onDeleteTodoItem = (id) => {
      todos.value=todos.value.filter(item=>item.id!==id)

    };

    const createTodo = (data) =>{
      const dataTodo = {
        id: todos.value.length+1,
        title: data,
        completed: false
      }

      todos.value.push(dataTodo)
      
    }

    return { checkedName, onChecked, onDeleteTodoItem, todos, createTodo };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.header {
  height: 200px;
  background-color: #333;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 72px;
  color: #fff;
}
</style>