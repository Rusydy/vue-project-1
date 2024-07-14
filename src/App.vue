<template>
  <h1>{{ title }}</h1>

  <h2>Add a new task</h2>

  <div>
    <input type="text" v-model="newTask" placeholder="Add a new task" @keyup.enter="addTask">
    <button @click="addTask" :disabled="newTask.length < 1">Add task</button>
  </div>

  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.id }}. {{ task.name }}
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