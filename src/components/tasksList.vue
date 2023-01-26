<template>
  <div class="card customTask" style="width: 18rem">
    <ul class="contentTask">
      <li v-for="(task, index) in props.tasks" :key="task" class="listStyle">
        <div style="margin: 5px; display: flex">
          <div class="form-check form-switch">
            <input
              @click="doneTASK(index)"
              class="form-check-input"
              type="checkbox"
              id="flexSwitchCheckDefault"
            />
          </div>
          <span v-if="!task.isDone">{{ task.task }}</span>
          <span v-else>
            <del>{{ task.task }}</del>
          </span>
        </div>
        <span>
          <div class="flexButtom">
            <div>
              <button
                @click="deleteTASK(index)"
                type="button"
                class="btn btn-danger buttomCustom"
              >
                X
              </button>
            </div>
          </div>
        </span>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";
//TOMANDO LA PROP MANDADA POR EL COMPONENTE PADRE
const props = defineProps({
  tasks: Array,
});
//TOMANDO LA FUNCION MANDADA POR EL COMPONENTE PADRE
const emit = defineEmits(["deleteTask", "doneTask"]);
//EMITIENDO LA PETICION AL COMPONENTE PADRE PARA USAR LAS FUNCIONES DE BORRAR Y "REALIZADO"
const deleteTASK = (index) => {
  emit("deleteTask", index);
};
const doneTASK = (index) => {
  emit("doneTask", index);
};
</script>

<style scoped>
.listStyle {
  color: antiquewhite;
  display: flex;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: space-between;
  border: 2px transparent gray;
  border-radius: 5px;
  margin: 5px;
  background-color: rgb(52, 47, 78);
  width: 80%;
}

.customTask {
  margin-bottom: 20px;
  background-color: rgb(38, 35, 54);
}
.flexButtom {
  display: flex;
  flex-wrap: nowrap;
  margin: 5px;
}
.buttomCustom {
  width: 25px;
  height: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black;
  border: 1px solid black;
}
.contentTask {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(38, 35, 54);
  padding-left: 0px;
}
@media (min-width: 769px) {
  .listStyle {
    width: 400px;
    margin-left: 220px;
  }
}
</style>
