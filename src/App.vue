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
    <ol>
      <li v-for="toDo in toDoItems" :key="toDo.timestamp">
        {{ toDo.text }}
      </li>
    </ol>
    <!--
    <ListItems
      items="{this.state.toDoItems}"
      deleteItem="{this.deleteItem}"
      markItemComplete="{this.markItemComplete}"
      clearCompleted="{this.clearCompleted}"
    />
    -->
  </div>
</template>

<script>
import Vue from "vue";
import { library } from "@fortawesome/fontawesome-svg-core";
import { faPlusCircle } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import "./assets/sass/bulma-import.scss";
import "./assets/sass/global.scss";

library.add(faPlusCircle);
Vue.component("font-awesome-icon", FontAwesomeIcon);

export default {
  name: "ToDoVue",
  data: function() {
    return {
      newUserItem: "",
      toDoItems: [{ text: "this" }, { text: "that" }]
    };
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
    }
  }
};
</script>

<style lang="scss"></style>
