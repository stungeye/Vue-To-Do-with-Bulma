<template>
  <nav class="panel is-info">
    <p class="panel-heading">Things You Need To Do</p>

    <p v-if="toDoItems.length === 0" class="panel-block">
      You having nothing to do yet.
    </p>

    <div v-for="toDo in toDoItems" :key="toDo.timestamp" class="panel-block">
      <label class="control is-expanded">
        <input
          type="checkbox"
          :checked="toDo.done"
          @change="$emit('toggle-item-completion', toDo)"
        />
        <del v-if="toDo.done">{{ toDo.text }}</del>
        <span v-else>{{ toDo.text }}</span>
      </label>

      <button
        class="button is-danger is-small is-light"
        @click="$emit('delete-item', toDo)"
      >
        <font-awesome-icon icon="trash" />
      </button>
    </div>

    <div v-if="toDoItems.length !== 0" class="panel-block">
      <button
        class="button is-link is-outlined is-fullwidth is-danger"
        @click="$emit('clear-completed-items')"
      >
        <font-awesome-icon icon="broom" /> &nbsp; Clear Complete Items
      </button>
    </div>
  </nav>
</template>

<script>
import { library } from "@fortawesome/fontawesome-svg-core";
import { faTrash, faBroom } from "@fortawesome/free-solid-svg-icons";

library.add(faTrash, faBroom);

export default {
  name: "ListItems",
  props: {
    toDoItems: {
      type: Array,
      default: () => {
        [];
      }
    }
  }
};
</script>
