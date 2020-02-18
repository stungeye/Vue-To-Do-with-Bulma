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
          <!--<FontAwesomeIcon icon="{faPlusCircle}" /> -->
          ADD
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
import "./assets/sass/bulma-import.scss";
import "./assets/sass/global.scss";

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
