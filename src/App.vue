<template>
  <img :src="logoURL" :alt="logoCaption" width="200" height="200" />

  <h1>{{ title }}</h1>

  <h2>Add a new task</h2>

  <span>You have {{ allTasks }} {{ allTasks > 1 ? 'tasks' : 'task' }} at the moment</span>

  <div>
    <input type="text" v-model="newTask" placeholder="Add a new task" @keyup.enter="addTask">
    <button @click="addTask" :disabled="newTask.length < 1">Add task</button>
  </div>

  <ul>
    <li v-for="(task, index) in latestTask" :key="index" @click.stop="toggleTask(task.id)"
      :class="{ strikeout: task.finished }">
      {{ index + 1 }}. {{ task.name }}

      <button @click.stop="removeTask(task.id)">Remove</button>
      <button @click.stop="toggleTask(task.id)">
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
      logoURL: 'https://images.unsplash.com/photo-1507925921958-8a62f3d1a50d?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1955&q=80',
      logoCaption: 'A photo by Kelly Sikkema on Unsplash showing post-it notes',
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
  },
  computed: {
    allTasks() {
      return this.tasks.length
    },
    latestTask() {
      return [...this.tasks].reverse()
    }
  }
}
</script>

<style>
.strikeout {
  text-decoration: line-through;
}
</style>