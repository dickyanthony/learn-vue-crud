<script>
//OPTIONS API
export default {
  data() {
    return {
      name: "John Doe",
      status: "pending",
      tasks: ["Task one", "Task two", "Task three"],
      link: "https://www.google.com/",
    };
  },
  methods: {
    toggleStatus() {
      console.log("click==>");
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>
<template>
  <h1>name: {{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is incative</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" v-bind:key="task">{{ task }}</li>
    <a :href="link">Click to google</a>
    <!-- <button v-on:click="toggleStatus">Change status</button> -->
    <button @click="toggleStatus">Change status</button>
  </ul>
</template>
