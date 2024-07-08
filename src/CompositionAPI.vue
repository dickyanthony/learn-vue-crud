<script setup>
import { onMounted, ref } from "vue";

const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["task1", "task2", "task3"]);
const newTask = ref("aad");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

function addTask() {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
}

const deleteTask = (indexProps) => {
  // const modifyNewTask = tasks.value.filter(
  //   (item, index) => indexProps !== index
  // );
  // tasks.value = modifyNewTask;
  tasks.value.splice(indexProps, 1);
};

onMounted(async () => {
  fetch("https://jsonplaceholder.typicode.com/todos")
    .then((response) => {
      return response.json();
    })
    .then((result) => {
      console.log("data==>", result);
      tasks.value = result.map((task) => task.title);
    })
    .catch((error) => console.log(error));
});
</script>

<template>
  <h1>name: {{ name }}</h1>

  <p v-if="status === 'active'">Status is active</p>
  <p v-else-if="status === 'pending'">Status is pending</p>
  <p v-else>Status is inactive</p>
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>
  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">delete</button>
    </li>
  </ul>
  <a :href="link">Click google</a>
  <br />
  <button @click="toggleStatus">Change status</button>

  <!-- <button v-on:click="toggleStatus">Change status</button> -->
</template>
