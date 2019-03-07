<template>
  <div>
    <div class="list-info">
      <v-btn class="nav-btn" v-if="completed.length > 0" @click="toggleShowComplete">
        <span v-if="!showComplete">Show</span>
        <span v-else>Hide</span>
        -Completed:{{ todos.filter(todo => { return todo.done }).length }}
      </v-btn>
      <v-btn class="nav-btn" v-if="pending.length > 0" @click="toggleShowPending">
        <span v-if="!showPending">Show</span>
        <span v-else>Hide</span>
        -Pending: {{ todos.filter(todo => { return !todo.done }).length }}
      </v-btn>
      <v-btn class="nav-btn" v-if="priority.length > 0" @click="toggleShowPriority">
        <span v-if="!showPriority">Show</span>
        <span v-else>Hide</span>
        -Priority: {{ todos.filter(todo => { return todo.priority }).length }}
      </v-btn>
      <v-btn class="nav-btn" @click="showAll">Show All</v-btn>
      <v-btn class="nav-btn" @click="sortDueDate">Due dates</v-btn>
      <v-btn class="nav-btn" @click="sortCreatedDate">Created dates</v-btn>
    </div>
    <div v-if="completed.length > 0 && showComplete">
      <CompleteTodoItem v-for="(todo,index) in completed" v-bind:todo="todo" v-bind:key="index"/>
    </div>
    <div v-else-if="pending.length > 0 && showPending">
      <CompleteTodoItem v-for="(todo,index) in pending" v-bind:todo="todo" v-bind:key="index"/>
    </div>
    <div v-else-if="priority.length > 0 && showPriority">
      <CompleteTodoItem v-for="(todo,index) in priority" v-bind:todo="todo" v-bind:key="index"/>
    </div>
    <div v-else-if="sortDueComputed.length > 0 && sortDue">
      <CompleteTodoItem
        v-for="(todo,index) in sortDueComputed"
        v-bind:todo="todo"
        v-bind:key="index"
      />
    </div>
    <div v-else-if="sortCreatedComputed.length > 0 && sortCreated">
      <CreatedDatetodo
        v-for="(todo,index) in sortCreatedComputed"
        v-bind:todo="todo"
        v-bind:key="index"
      />
    </div>
    <div v-else-if="!showComplete && !showPending && !showPriority && !sortDue && !sortCreated">
      <TodoItem
        v-on:delete-todo="deleteTodo"
        v-on:complete-todo="completeTodo"
        v-for="(todo,index) in todos"
        v-bind:todo="todo"
        v-bind:key="index"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
import CompleteTodoItem from "./CompleteTodoItem.vue";
import CreatedDatetodo from "./CreatedDatetodo.vue";
export default {
  props: ["todos"],
  components: {
    TodoItem,
    CompleteTodoItem,
    CreatedDatetodo
  },
  data() {
    return {
      showComplete: false,
      showPending: false,
      showPriority: false,
      sortDue: false,
      sortCreated: false
    };
  },
  computed: {
    completed: function() {
      return this.todos.filter(function(item) {
        return item.done;
      });
    },
    pending: function() {
      return this.todos.filter(function(item) {
        return !item.done;
      });
    },
    priority: function() {
      return this.todos.filter(function(item) {
        return item.priority;
      });
    },
    sortDueComputed: function() {
      const copyTodo = [...this.todos];
      return copyTodo.sort(function(a, b) {
        return new Date(a.dueDate) - new Date(b.dueDate);
      });
    },
    sortCreatedComputed: function() {
      const deepTodo = [...this.todos];
      return deepTodo.sort(function(a, b) {
        return new Date(a.createdDate) - new Date(b.createdDate);
      });
    }
  },
  methods: {
    showAll() {
      this.showComplete = false;
      this.showPending = false;
      this.showPriority = false;
      this.sortDue = false;
      this.sortCreated = false;
    },
    sortDueDate() {
      this.showComplete = false;
      this.showPending = false;
      this.showPriority = false;
      this.sortCreated = false;
      this.sortDue = true;
    },
    sortCreatedDate() {
      this.showComplete = false;
      this.showPending = false;
      this.showPriority = false;
      this.sortDue = false;
      this.sortCreated = true;
    },
    toggleShowComplete() {
      this.sortDue = false;
      this.sortCreated = false;
      this.showPending = false;
      this.showPriority = false;
      this.showComplete = !this.showComplete;
    },
    toggleShowPending() {
      this.sortDue = false;
      this.showPriority = false;
      this.sortCreated = false;
      this.showComplete = false;

      this.showPending = !this.showPending;
    },
    toggleShowPriority() {
      this.sortDue = false;
      this.sortCreated = false;
      this.showComplete = false;
      this.showPending = false;
      this.showPriority = !this.showPriority;
    },
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
    }
  }
};
</script>

<style  scoped>
.list-info {
  margin: 2rem;
  text-align: center;
}
</style>
