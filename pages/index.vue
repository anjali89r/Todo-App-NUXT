<template>
  <div>
    <v-layout row justify-center align-center>
      <v-flex xs12 sm8 md6>
        <div>
          <TodoList :todos="todos"/>
          <CreateTodo @create-todo="addTodo"/>
        </div>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import TodoList from "../components/TodoList.vue";
import CreateTodo from "../components/CreateTodo.vue";
export default {
  name: "app",
  components: {
    TodoList,
    CreateTodo
  },
  data() {
    return {
      todos: [
        {
          title: "Todo A",
          project: "Project A",
          dueDate: "2019/03/23",
          createdDate: "2019/02/11",
          priority: false,
          done: false
        },
        {
          title: "Todo B",
          project: "Project B",
          dueDate: "2019/03/12",
          createdDate: "2019/01/17",
          priority: false,
          done: false
        },
        {
          title: "Todo C",
          project: "Project C",
          dueDate: "2019/03/13",
          createdDate: "2019/02/30",
          priority: true,
          done: false
        }
      ]
    };
  },

  methods: {
    addTodo(todo) {
      console.log("addtodo");
      this.todos.push(todo);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
