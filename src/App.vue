<script setup>
import { onMounted, ref } from "vue";

const name = ref("Tarun");
const status = ref("Active");
const tasks = ref(["Task 1", "Task 2", "Task 3"]);
const newTask = ref("");


const toggleStatus = () => {
  if (status.value === "Active") {
    status.value = "Inactive";
  } else if (status.value === "Inactive") {
    status.value = "Pending";
  } else {
    status.value = "Active";
  }

};
const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value.trim());
    newTask.value = "";
  }
};
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async()=>{
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
    console.log(data);
  } catch (error) {
    console.error("Error fetching data:", error);
    
  }
})
</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'Active'">user is active</p>
  <p v-else-if="status === 'Pending'">user is pending</p>
  <p v-else>user is inactive</p>

  <form action="" @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" v-model="newTask" />
    <button type="submit">Add</button>
  </form>
  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }} </span>
      <!-- <button @click="tasks.splice(tasks.indexOf(task), 1)">Delete</button> -->
      <button @click=deleteTask(index)>Delete</button>
    </li>
  </ul>
  <!-- <a v-bind:href="link">Click Me</a> -->
  <br />
  <button @click="toggleStatus">change status</button>
</template>
