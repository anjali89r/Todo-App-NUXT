<template>
  <div class="ui centered card">
    <!-- // Todo shown when we are not in editing mode. -->
    <div class="content" v-show="!isEditing">
      <transition name="fade" mode="out-in">
        <v-card
          :class="{ 'card-priority': todo.priority, 'mx-auto': true}"
          class="point card-hover"
          max-width="400"
          @click="flip = !flip"
          v-if="!flip"
          key="brief"
        >
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
          <!-- <v-card-text class="headline font-weight-bold">
      {{ todo.title }}
          </v-card-text>-->
          <v-card-actions>
            <v-list-tile class="grow">
              <v-list-tile-content>
                <v-btn outline color="cyan" @click="showForm" v-show="!todo.done">
                  <v-icon>edit</v-icon>
                </v-btn>
                <v-btn outline color="red" @click.stop="deleteTodo(todo)" v-show="todo.done">
                  <v-icon class="mr-1">delete</v-icon>
                </v-btn>
              </v-list-tile-content>

              <v-layout align-center justify-end>
                <v-btn
                  block
                  color="secondary"
                  dark
                  v-show="!isEditing && !todo.done"
                  @click.stop="completeTodo(todo)"
                >Pending</v-btn>
                <v-btn
                  block
                  :disabled="!isEditing && todo.done"
                  color="info"
                  dark
                  v-show="!isEditing && todo.done"
                >Completed</v-btn>
              </v-layout>
            </v-list-tile>
            <v-btn icon @click.stop="show = !show">
              <v-icon>{{ show ? 'keyboard_arrow_down' : 'keyboard_arrow_up' }}</v-icon>
            </v-btn>
          </v-card-actions>
          <v-slide-y-transition>
            <v-card-text v-show="show">Todo created on {{todo.createdDate}}</v-card-text>
          </v-slide-y-transition>
        </v-card>
        <DetailTodo :todo="todo" @toggleFlip="flip = !flip" v-if="flip" key="detail"/>
      </transition>
    </div>

    <!-- // form is visible when we are in editing mode -->
    <v-card class="mx-auto" max-width="400" v-show="isEditing">
      <v-card-text>
        <v-form>
          <v-container>
            <v-layout>
              <v-flex xs10>
                <v-text-field v-model="todo.title" label="Title" required></v-text-field>
              </v-flex>
              <v-flex xs2>
                <div class="point" @click.stop="todo.priority = !todo.priority">
                  <v-icon :class="{urgent: todo.priority}">star</v-icon>
                </div>
              </v-flex>
            </v-layout>
            <v-layout>
              <v-flex xs12>
                <v-textarea solo name="input-7-4" label="Description" v-model="todo.project"></v-textarea>
              </v-flex>
            </v-layout>
            <v-layout>
              <v-flex xs12>
                <v-menu
                  lazy
                  v-model="menu"
                  transition="scale-transition"
                  offset-y
                  full-width
                  :nudge-right="40"
                  max-width="290px"
                  min-width="290px"
                >
                  <v-text-field
                    slot="activator"
                    label="Picker in menu"
                    v-model="date"
                    prepend-icon="event"
                    readonly
                  ></v-text-field>
                  <v-date-picker v-model="date" no-title scrollable actions></v-date-picker>
                </v-menu>
              </v-flex>
            </v-layout>
          </v-container>
        </v-form>
      </v-card-text>

      <v-card-actions>
        <v-list-tile class="grow">
          <!-- <v-list-tile-content>
          <v-btn  class="mx-auto" color="warning" @click="hideForm">Close</v-btn>
          </v-list-tile-content>-->
          <v-layout align-center>
            <v-btn class="mx-auto" color="warning" @click.stop="hideForm">Save</v-btn>
          </v-layout>
        </v-list-tile>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
import moment from "moment";
import DetailTodo from "./DetailTodo.vue";
export default {
  props: ["todo"],
  components: {
    DetailTodo
  },
  data() {
    return {
      isEditing: false,
      date: new Date().toISOString().substr(0, 10),
      menu: false,
      modal: false,
      show: false,
      flip: false
    };
  },
  //computed: {
  //     dateFormated() {

  //       this.todo.dueDate = moment(this.date).format('MM/DD/YYYY');
  //       return this.todo.dueDate;
  //       //return moment(this.date).format('MM/DD/YYYY');
  //     }
  //   },
  methods: {
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.todo.dueDate = this.date;
      this.isEditing = false;
    },
    deleteTodo(todo) {
      this.$emit("delete-todo", todo);
    },
    completeTodo(todo) {
      this.$emit("complete-todo", todo);
    }
  }
};
</script>

<style scoped>
.button[disabled] {
  cursor: not-allowed;
}
.theme--dark.v-btn.v-btn--disabled:not(.v-btn--icon):not(.v-btn--flat):not(.v-btn--outline) {
  background-color: #469689 !important;
  cursor: not-allowed !important;
  color: #fff !important;
}
i {
  cursor: pointer;
}
</style>
