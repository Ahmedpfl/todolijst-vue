<script setup>
import { ref, computed, watch } from "vue";

const task_name = ref('');
const task_description = ref('');
const tasks = ref(JSON.parse(localStorage.getItem('tasks')) || [
  { id: 1, title: "shower", description: "you should go and take a shower", done: false },
  { id: 2, title: "eat", description: "you need to eat some food", done: false },
]);

const todoTasks = computed(() => tasks.value.filter(task => !task.done));
const doneTasks = computed(() => tasks.value.filter(task => task.done));

function addTask() {
  if (task_name.value.trim() === '') return;
  tasks.value.push({
    id: Date.now(),
    title: task_name.value,
    description: task_description.value,
    done: false,
  });
  task_name.value = '';
  task_description.value = '';
}

function toggleDone(id) {
  const task = tasks.value.find(task => task.id === id);
  task.done = !task.done;
}

function removeTask(id) {
  tasks.value = tasks.value.filter(task => task.id !== id);
}

watch(tasks, (value) => {
  localStorage.setItem('tasks', JSON.stringify(value));
}, { deep: true });
</script>

<template>
  <main class="todo">
    <h1>Todo-list</h1>

    <div class="form">
      <input type="text" v-model="task_name" placeholder="Title" />
      <input type="text" v-model="task_description" placeholder="Description" />
      <button @click="addTask">Add task</button>
    </div>

    <section>
      <h2>To do <span class="count">{{ todoTasks.length }}</span></h2>
      <p v-if="todoTasks.length === 0" class="empty">Nothing to do.</p>
      <div class="task" v-for="task in todoTasks" :key="task.id">
        <div>
          <p class="task-title">{{ task.title }}</p>
          <p class="task-desc">{{ task.description }}</p>
        </div>
        <button @click="toggleDone(task.id)">Done</button>
      </div>
    </section>

    <section>
      <h2>Done <span class="count">{{ doneTasks.length }}</span></h2>
      <p v-if="doneTasks.length === 0" class="empty">Nothing done yet.</p>
      <div class="task finished" v-for="task in doneTasks" :key="task.id">
        <div>
          <p class="task-title">{{ task.title }}</p>
          <p class="task-desc">{{ task.description }}</p>
        </div>
        <div class="actions">
          <button class="ghost" @click="toggleDone(task.id)">Undo</button>
          <button class="ghost" @click="removeTask(task.id)">Delete</button>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
:global(body) {
  background: white;
  font-family: system-ui, sans-serif;
}

.todo {
  max-width: 460px;
  margin: 40px auto;
  padding: 24px;
  background: #42b883;
  color: white;
  border-radius: 16px;
}

h1 {
  text-align: center;
  margin: 0 0 20px;
}

h2 {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 18px;
  margin: 24px 0 10px;
}

.count {
  background: #35495e;
  border-radius: 99px;
  padding: 2px 10px;
  font-size: 14px;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

input {
  padding: 10px 12px;
  border: 0;
  border-radius: 8px;
  font-size: 16px;
}

button {
  padding: 10px 14px;
  border: 0;
  border-radius: 8px;
  background: #35495e;
  color: white;
  font-size: 15px;
  cursor: pointer;
}

button:hover {
  background: #2c3e50;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  background: white;
  color: #222;
  border-radius: 10px;
  padding: 12px 14px;
  margin-bottom: 8px;
}

.task-title {
  font-weight: bold;
  margin: 0;
}

.task-desc {
  margin: 2px 0 0;
  color: #666;
  font-size: 14px;
}

.finished .task-title {
  text-decoration: line-through;
  color: #888;
}

.actions {
  display: flex;
  gap: 6px;
}

.ghost {
  background: #e8ecef;
  color: #35495e;
}

.ghost:hover {
  background: #d8dee3;
}

.empty {
  margin: 0;
  font-size: 14px;
}
</style>
