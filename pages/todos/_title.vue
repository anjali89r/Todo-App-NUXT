<template>
  <div class='ui centered card'>
    <!-- // Todo shown when we are not in editing mode. -->
    <div class="content">
      <v-card
    :class="{ 'card-priority': todo.priority, 'mx-auto': true}"
    class="point"
    max-width="400"
   @click="flipCard"
  >
    <v-card-title>

     <div>

         <span class="headline font-weight-bold">{{ todo.title }}</span>
         <span v-show="todo.priority"><v-icon :class="{urgent: todo.priority}">star</v-icon></span><br>
         <span>priority: <span v-if="todo.priority" class="priority-font"> Important</span>
         <span v-else class="general-font"> Low</span></span><br>
            <span>{{ todo.project }}</span><br>
            <span>Due Date: {{todo.dueDate}}</span><br>
            <span>Created on {{todo.createdDate}}</span>
          </div>
    </v-card-title>

    <!-- <v-card-text class="headline font-weight-bold">
      {{ todo.title }}
    </v-card-text> -->

    <v-card-actions>
      <v-list-tile class="grow">
        <v-layout
          align-center

        >
         <v-chip v-if="todo.done" color="green" text-color="white">Completed</v-chip>
          <v-chip v-else-if="!todo.done" color="orange" text-color="white">Pending</v-chip>

        </v-layout>
      </v-list-tile>

    </v-card-actions>

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
  },
methods: {
   flipCard() {
      this.$emit('toggleFlip');
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
