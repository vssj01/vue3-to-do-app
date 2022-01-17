<template>
  <h1>Todo App</h1>
  <form @submit.prevent="addToDo">
    <label>New To Do</label>
    <input v-model="newTodo" name="newTodo" />
    <button>Add</button>
  </form>
  <h2>To Do List</h2>
  <ul>
    <li v-for="(todo, index) in todos" :key="index">
      <span @click="doneToDo(todo)" :class="{ done: todo.done }">{{
        todo.content
      }}</span>

      <button @click="isEdit = !isEdit">Edit</button>

      <button @click="removeToDo(index)">Remove</button>
      <EditTodo
        v-if="isEdit"
        :todo="todo"
        @closeModal="closeModal"
        :key="index"
      >
        <input v-model="todo.content" @keydown.enter="isEdit = false" />
      </EditTodo>
    </li>
  </ul>
  <h4 v-if="todos.length === 0">Empty List</h4>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import EditTodo from "../components/EditTodo.vue";
export default defineComponent({
  components: { EditTodo },
  setup() {
    const newTodo = ref("");
    let isEdit = ref(false);
    const defaultData = [{ done: false, content: "default todo" }];
    const todos = ref(defaultData);

    const addToDo = () => {
      if (newTodo.value) {
        todos.value.push({
          done: false,
          content: newTodo.value,
        });
        newTodo.value = "";
      }
    };

    function removeToDo(index: number) {
      todos.value.splice(index, 1);
    }

    function doneToDo(todo: any) {
      todo.done = !todo.done;
    }

    function closeModal() {
      isEdit.value = false;
    }
    return {
      newTodo,
      todos,
      addToDo,
      removeToDo,
      doneToDo,
      isEdit,
      closeModal,
    };
  },
});
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
