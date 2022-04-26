<template>
  <div class="totoContainer">
   <input class="input" v-model="content" />
   <button class="create" @click="onClick">Create todo</button>
  </div>
</template>

<script>
import { ref } from "vue";


export default {
  name: "CreateTodo",
  props: [],

  setup(props, context) {
    const content = ref('')
    const onClick = () =>{
        context.emit('onClickCreate', content.value)
        content.value=''
    }
    return {onClick, content};
  },
};
</script>

<style scoped>
.totoContainer {
  display: flex;
  padding: 10px 20px;
  align-items: center;
}



.input {
  flex-grow: 1;
  padding: 0 20px;
}

</style>