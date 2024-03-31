<script setup>

// client only methods
function readTasks() {
  try {
    const arr = JSON.parse(localStorage.getItem('tasks'));
    if (!Array.isArray(arr)) throw new Error('"tasks" in local storage is not array')
    return JSON.parse(localStorage.getItem('tasks')); // array of tasks
  } catch {
    return []
  }
}
function saveTasks(arr) {
  localStorage.setItem('tasks', JSON.stringify(arr));
}
const loading = ref(true);
const tasks = ref([]);

// changing state methods
// it is below state so we can modify it
const addTask = ({ title, description }) => {
  tasks.value.push({
    id: new Date().getTime(),
    title,
    description
  })
  saveTasks(tasks.value);
}

const deleteTask = (id) => {
  tasks.value = tasks.value.filter((item) => item.id !== id);
  saveTasks(tasks.value);
}

const updateTask = (updatedTask) => {
  console.log(updatedTask);
  tasks.value = tasks.value.map((task) => task.id === updatedTask.id ? updatedTask : task)
  saveTasks(tasks.value);
}

onMounted(() => {
  loading.value = false;
  tasks.value = readTasks();
})
</script>

<template>
  <div>
    <h1 class="text-3xl font-bold">Tasks</h1>
    <div>
      <div v-if="loading">
        loading...
      </div>
      <div v-if="!loading">
        <div class="tasks my-2">
          <Task v-for="task in tasks" :task="task" @delete="deleteTask" @save="updateTask" />
        </div>
      </div>
      <AddTask class="p-5" @add-task="addTask" />
    </div>
  </div>
</template>

<style>
.tasks {
  background: #d8d8d8;
  min-height: 50px;
  padding: 10px;
}
</style>