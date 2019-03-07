<template>
  <div class="ui centered card">
    <div class="content">
      <v-card
        :class="{ 'card-priority': todo.priority, 'mx-auto': true}"
        class="point card-hover"
        max-width="400"
        @click="flipCard"
      >
        <v-layout row>
          <v-flex xs12>
            <v-card-title primary-title>
              <div>
                <div class="headline">{{ todo.title }}</div>
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
                <v-chip v-if="todo.done" color="green" text-color="white">Completed</v-chip>
                <v-chip v-else-if="!todo.done" color="orange" text-color="white">Pending</v-chip>
              </div>
            </v-card-text>
          </v-flex>
        </v-layout>
        <v-divider light></v-divider>
        <v-card-actions class="pa-3">
          <span class="general-font">Due: {{todo.dueDate}}</span>
          <v-spacer></v-spacer>
          <span class="general-font">Created: {{todo.createdDate}}</span>
          <v-btn icon @click.stop="show = !show">
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
</template>

<script>
export default {
  props: ["todo"],
  data() {
    return {
      show: true
    };
  },
  methods: {
    flipCard() {
      this.$emit("toggleFlip");
    }
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
