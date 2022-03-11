<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    const inputText = "";
    const todoList: Array<{ taskName: string; checked: boolean }> =
      JSON.parse(localStorage.getItem("todoList")!) || [];

    return {
      inputText,
      todoList,
    };
  },
  methods: {
    addTask(event: Event): void {
      event.preventDefault();

      if (!this.inputText.length) return;

      this.todoList.push({ taskName: this.inputText, checked: false });

      this.inputText = "";

      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
    deleteTask(index: number): void {
      this.todoList.splice(index, 1);
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
    checkTask(index: number): void {
      if (this.todoList[index].checked) {
        this.todoList[index].checked = false;
      } else {
        this.todoList[index].checked = true;
      }

      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
  },
});
</script>

<template>
  <h1>To Do</h1>
  <form @submit="addTask($event)">
    <input type="text" v-model="inputText" />

    <button class="add-task" type="submit">+</button>
  </form>
  <div id="tasks">
    <p v-if="!todoList.length">Empty List</p>
    <div class="task" v-for="(task, index) in todoList" :key="index">
      <input
        type="checkbox"
        :checked="task.checked"
        @change="checkTask(index)"
      />
      <p :class="task.checked && 'checked'">
        {{ task.taskName }}
      </p>
      <button class="delete-task" @click="deleteTask(index)">x</button>
    </div>
  </div>
</template>

<style scoped lang="scss">
#tasks {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 90vw;
  max-width: 400px;

  .checked {
    text-decoration: line-through;
  }
}

input[type="checkbox"] {
  cursor: pointer;
}

input[type="text"] {
  border-right: none;
  border-top: 1px solid #999;
  border-left: 1px solid #999;
  border-bottom: 1px solid #999;
  outline: none;
  width: 60vw;
  max-width: 300px;
}

.add-task {
  background: transparent;
  border-right: 1px solid #999;
  border-left: none;
  border-top: 1px solid #999;
  border-bottom: 1px solid #999;
  transition: all 0.2s linear;
  cursor: pointer;

  &:hover {
    background: rgb(85, 158, 187);

    color: #fff;
  }
}

.delete-task {
  background: transparent;
  border: 1px solid #999;
  border-radius: 4px;
  cursor: pointer;
  padding-bottom: 2px;
  transition: all 0.2s linear;

  &:hover {
    background: rgb(187, 85, 85);
    border: 1px solid transparent;
    color: #fff;
  }
}
</style>
