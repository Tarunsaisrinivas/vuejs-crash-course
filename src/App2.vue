<script>
export default {
  data() {
    return {
      name: "Tarun",
      status: "Active",
      tasks: ["task1", "task2", "task3"],
      link: "https://www.example.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === "Active") {
        this.status = "Pending";
      } else if (this.status === "Pending") {
        this.status = "Inactive";
      } else {
        this.status = "Active";
      }
    },
  },
};
</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'Active'">user is active</p>
  <p v-else-if="status === 'Pending'">user is pending</p>
  <p v-else>user is inactive</p>
  <h3>Tasks:</h3>
  <ul>

    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <a v-bind:href="link">Click Me</a>
  <br>
  <button @click = "toggleStatus">{{ status }}</button>
</template>
