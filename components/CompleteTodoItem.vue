<template>
  <div class="ui centered card">
    <div class="content">
      <v-card :class="{ 'card-priority': todo.priority, 'mx-auto': true}" max-width="400">
        <v-card-title>
          <div>
            <span class="headline font-weight-bold">{{ todo.title }}</span>
            <span v-show="todo.priority">
              <v-icon :class="{urgent: todo.priority}">star</v-icon>
            </span>
          </div>
        </v-card-title>

        <v-card-text>
          <span>
            priority:
            <span v-if="todo.priority" class="priority-font">Important</span>
            <span v-else class="general-font">Low</span>
          </span>
          <br>
          <div class="mt8">
            <span class="general-font">Due: {{todo.dueDate}}</span>
          </div>
        </v-card-text>

        <v-card-actions>
          <v-list-tile class="grow">
            <v-layout align-center>
              <v-chip v-if="todo.done" color="green" text-color="white">Completed</v-chip>
              <v-chip v-else-if="!todo.done" color="orange" text-color="white">Pending</v-chip>
            </v-layout>
          </v-list-tile>
          <v-btn icon @click="show = !show">
            <v-icon>{{ show ? 'keyboard_arrow_down' : 'keyboard_arrow_up' }}</v-icon>
          </v-btn>
        </v-card-actions>
        <v-slide-y-transition>
          <v-card-text class="card-text" v-show="show">
            <h4>Description</h4>
            <p>{{ todo.project }}</p>
          </v-card-text>
        </v-slide-y-transition>
      </v-card>
    </div>
  </div>
  <!-- // form is visible when we are in editing mode -->
</template>

<script>
export default {
  props: ["todo"],
  data() {
    return {
      show: false
    };
  }
};
</script>

<style scoped>
.button[disabled] {
  cursor: not-allowed;
}
i {
  cursor: pointer;
}
</style>
