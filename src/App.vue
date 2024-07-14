<template>
  <h1>{{ title }}</h1>

  <h2>Add a new task</h2>

  <div>
    <input type="text" v-model="newTask" placeholder="Add a new task">
    <button @click="addTask">Add task</button>
  </div>

  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.id }}. {{ task.name }}

      <div v-if="task.finished">
        <button>Delete task</button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      title: 'My To Do App',
      newTask: '',
      tasks: [
        { id: 1, name: 'Learn Vue JS', finished: false },
        { id: 2, name: 'Build a Vue application', finished: false },
        { id: 3, name: 'Write an article about Vue JS', finished: false }
      ]
    }
  },
  methods: {
    addTask() {
      if (this.newTask.length < 1) return

      this.tasks.push({
        id: this.tasks.length + 1,
        name: this.newTask,
        finished: false
      });

      this.newTask = ''
    }
  }
}
</script>