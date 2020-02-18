<template>
  <div id="app">
    <div class="field has-addons">
      <div class="control is-expanded">
        <input
          v-model.trim="newUserItem"
          class="input"
          placeholder="What do you need to do?"
          @keyup.enter="addNewUserItem"
        />
      </div>

      <div class="control">
        <button class="button is-primary" @click="addNewUserItem">
          <font-awesome-icon icon="plus-circle" />
        </button>
      </div>
    </div>

    <list-items
      :to-do-items="toDoItems"
      @delete-item="deleteItem"
      @toggle-item-completion="toggleItemCompletion"
      @clear-completed-items="clearCompletedItems"
    />
  </div>
</template>

<script>
import Vue from "vue";
import { library } from "@fortawesome/fontawesome-svg-core";
import { faPlusCircle } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ListItems from "@/components/ListItems.vue";
import serializedStorage from "@/serializedStorage.js";

import "./assets/sass/bulma-import.scss";
import "./assets/sass/global.scss";

library.add(faPlusCircle);
Vue.component("font-awesome-icon", FontAwesomeIcon);

export default {
  name: "ToDoVue",
  components: { ListItems },

  data: function() {
    return {
      newUserItem: "",
      toDoItems: serializedStorage.fetch()
    };
  },

  watch: {
    toDoItems: {
      handler: serializedStorage.save,
      deep: true
    }
  },

  methods: {
    addNewUserItem: function() {
      if (this.newUserItem === "") return;

      this.toDoItems.push({
        text: this.newUserItem,
        done: false,
        timestamp: Date.now()
      });

      this.newUserItem = "";
    },

    clearCompletedItems: function() {
      this.toDoItems = this.toDoItems.filter(toDo => !toDo.done);
    },

    deleteItem: function(toDo) {
      this.toDoItems = this.toDoItems.filter(
        item => item.timestamp !== toDo.timestamp
      );
    },

    toggleItemCompletion: function(toDo) {
      this.toDoItems = this.toDoItems.map(item => {
        if (item.timestamp === toDo.timestamp) {
          item.done = !item.done;
        }
        return item;
      });
    }
  }
};
</script>
