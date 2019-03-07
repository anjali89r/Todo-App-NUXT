<template>
  <div>
    <div class="text-center">
      <v-btn fab color="warning" @click="openForm" v-show="!isCreating">
        <v-icon>add</v-icon>
      </v-btn>
    </div>
    <v-card class="mx-auto" max-width="400" v-show="isCreating">
      <v-card-text>
        <v-form>
          <v-container>
            <v-layout>
              <v-flex xs10>
                <v-text-field v-model="titleText" label="Title" required></v-text-field>
              </v-flex>
              <v-flex xs2>
                <div class="point" @click="priority = !priority">
                  <v-icon :class="{urgent: priority}">star</v-icon>
                </div>
              </v-flex>
            </v-layout>
            <v-layout>
              <v-flex xs12>
                <v-textarea solo name="input-7-4" label="Description" v-model="projectText"></v-textarea>
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
          <v-list-tile-content>
            <v-btn class="mx-auto" color="warning" @click="sendForm">Create</v-btn>
          </v-list-tile-content>

          <v-layout align-center justify-end>
            <v-btn class="mx-auto" color="warning" @click="closeForm">Cancel</v-btn>
          </v-layout>
        </v-list-tile>
      </v-card-actions>
    </v-card>
  </div>
</template>
<script>
import moment from "moment";
export default {
  data() {
    return {
      titleText: "",
      projectText: "",
      isCreating: false,
      priority: false,
      date: new Date().toISOString().substr(0, 10),
      dueTodo: "",
      menu: false,
      modal: false,
      createdDate: new Date().toISOString().substr(0, 10)
    };
  },
  computed: {
    dateFormated() {
      this.dueTodo = moment(this.date).format("MM/DD/YYYY");
      return moment(this.date).format("MM/DD/YYYY");
    }
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      if (this.titleText.length > 0 && this.projectText.length > 0) {
        const title = this.titleText;
        const project = this.projectText;
        //const dueDate = this.dueTodo;
        const dueDate = this.date;
        const createdDate = this.createdDate;
        const priority = this.priority;
        console.log("todo: ", {
          title,
          project,
          dueDate,
          createdDate,
          priority,
          done: false
        });
        this.$emit("create-todo", {
          title,
          project,
          dueDate,
          createdDate,
          priority,
          done: false
        });
        this.titleText = "";
        this.projectText = "";
        this.isCreating = false;
        this.priority = false;
        this.createdDate = "";
      }
    }
  }
};
</script>
<style>
</style>
