<template>
  <h1>
    {{ title }}
  </h1>

  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.id }}. {{ task.name }}

      <div v-if="task.finished">
        <button @click="task.finished = false">Delete Task</button>
      </div>
      <div v-else-if="task.edit">
        <button @click="task.edit = false">Edit</button>
      </div>
      <div v-else>
        <p>No button</p>
      </div>
    </li>
  </ul>

  <h2>
    Add a new task
  </h2>

  <div v-if="newTask.length > 0">
    <h3>
      New task preview
    </h3>

    <p>
      {{ newTask }}
    </p>

  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'My To Do App',
      tasks: [
        { id: 1, name: 'Learn Vue', finished: false },
        { id: 2, name: 'Learn Vuex', finished: false },
        { id: 3, name: 'Learn Vue Router', finished: false }
      ]
    }
  }
}
</script>
