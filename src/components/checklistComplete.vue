<template>
  <!-- SECCION INPUT FOR TASKS -->
  <div class="styleApp">
    <section class="flexApp" style="margin-bottom: 5px">
      <div class="headerList">
        <h1 class="titles">Checklist</h1>
        <div style="display: flex;">
          <input
            class="inputTask"
            @keyup.enter="addTask()"
            v-model="task"
            type="text"
            name="inputTask"
            placeholder="Add new task"
          />
          <button @click="addTask()" type="button" class=" buttomAdd">+</button>
        </div>
      </div>
    </section>
    <div style="margin-left: 33px">
      <h3 class="titles" style="text-align: start">List of tasks:</h3>
    </div>
    <!-- SECCION TASK LIST AND BUTTOMS, SON COMPONENT -->
    <section class:="flexApp">
      <tasksList :tasks="tasks" @deleteTask="deleteTask" @doneTask="doneTask" />
    </section>
  </div>
</template>

<script setup>
import tasksList from "./tasksList.vue";

import { ref, onMounted, onUpdated } from "vue";

const tasks = ref([]);
const task = ref("");

//FUNCTIONS FOR LOCALSTORAGE
onMounted(() => {
  if (JSON.parse(localStorage.getItem("tasks")) != null) {
    tasks.value = JSON.parse(localStorage.getItem("tasks"));
  } else {
    localStorage.setItem("tasks", JSON.stringify([]));
  }
});
onUpdated(() => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
});

//FUNCTIONS FOR NEW TASK, DELETE TASK AND DONE TASK
const addTask = () => {
  if (task.value != "") {
    tasks.value.push({ task: task.value, isDone: false });
    task.value = "";
  } else {
    return false;
  }
};
const deleteTask = (taskIndex) => {
  tasks.value = tasks.value.filter((item, index) => {
    if (index != taskIndex) {
      return item;
    }
  });
};
const doneTask = (taskIndex) => {
  tasks.value = tasks.value.filter((item, index) => {
    if (index === taskIndex) {
      item.isDone = !item.isDone;
    }
    return item;
  });
};
</script>

<style scoped>
.flexApp {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.styleApp {
  border: 2px solid gray;
  border-radius: 20px;
  background-color: rgb(38, 35, 54);
}
.headerList {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.titles {
  color: antiquewhite;
}
h3 {
  font-size: medium;
  margin-top: 20px;
}
.inputTask {
  background-color: transparent ;
  appearance: none ;
  border: none;
  outline: none;
  border-bottom: 2px solid antiquewhite;
  color: antiquewhite;
}
.buttomAdd{
  width: 25px;
  height: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 10px;
  margin-top: 3px;
  border: none;
  background-color:rgb(38, 35, 54);
  color: antiquewhite;
}
@media (min-width: 769px) {
  .styleApp{
    width: 500px;
    height: 300px;
  }
  h3{
    font-size: 20px;
    margin-left: 20px;
  }
}
</style>
