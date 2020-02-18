<template>
  <ol>
    <li v-for="toDo in toDoItems" :key="toDo.timestamp">
      {{ toDo.text }}
    </li>
  </ol>
</template>

<script>
import Vue from "vue";
import { library } from "@fortawesome/fontawesome-svg-core";
import { faTrash, faBroom } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

library.add(faTrash, faBroom);
Vue.component("font-awesome-icon", FontAwesomeIcon);

export default {
  name: "ListItems",
  props: {
    toDoItems: {
      type: Array,
      default: () => {
        [];
      }
    },
    deleteItem: {
      type: Function,
      default: () => {
        return;
      }
    }
  }
};
</script>

<style lang="scss"></style>
