<template>
  <h1>{{ title }}</h1>

  <h2>Add a new task</h2>

  <div>
    <input type="text" v-model="newTask" placeholder="Add a new task" @keyup.enter="addTask">
    <button @click="addTask" :disabled="newTask.length < 1">Add task</button>
  </div>

  <ul>
    <li v-for="(task, index) in tasks" :key="index">
      {{ index + 1 }}. {{ task.name }}

      <button @click="removeTask(task.id)">Remove</button>
      <button @click="toggleTask(task.id)">
        {{ task.finished ? 'Mark as unfinished' : 'Mark as finished' }}
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      title: 'My To Do App',
      newTask: '',
      nextTaskId: 1,
      tasks: []
    }
  },
  methods: {
    addTask() {
      if (this.newTask.length < 1) return

      this.tasks.push({
        id: this.nextTaskId,
        name: this.newTask,
        finished: false
      });

      this.nextTaskId++
      this.newTask = ''
    },
    removeTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId)
    },
    toggleTask(taskId) {
      this.tasks = this.tasks.map(task => {
        if (task.id === taskId) {
          task.finished = !task.finished
        }

        return task
      })
    }
  }
}
</script>