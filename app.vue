<template>
  <div class="container">
    <div class="list-header pt-3">
      <h1 class="fw-bold">Todo List</h1>
    </div>
    <div v-if="tasks.length === 0">Belum ada task</div>
    <div class="list-task" v-else>
      <div
        v-for="(task, index) of tasks"
        :key="index"
        class="item-task d-flex align-items-start border-bottom pt-3 pb-4"
      >
        <input
          type="checkbox"
          name="status"
          id="task"
          class="me-2 mt-2"
          :checked="task.isDone"
          @change="toggleTaskStatus(task)"
        />
        <div class="d-flex flex-column">
          <div class="title-task mb-1" :class="{ checked: task.isDone }">
            {{ task.title }}
          </div>

          <div class="description-task small text-muted">
            {{ task.description }}
          </div>
          <a href="#" @click="deleteTask(index)">Delete</a>
        </div>
      </div>
    </div>
    <div class="action py-2">
      <a href="#" class="add-button" v-if="!isCreating" @click="toggleCreating"
        >Add Task</a
      >
      <div class="add-card" v-else>
        <div class="card mb-2">
          <div class="card-body d-flex flex-column p-2">
            <input
              class="form-control mb-2"
              placeholder="Title"
              type="text"
              v-model="title"
            />
            <textarea
              class="form-control small"
              placeholder="Description"
              rows="3"
              v-model="description"
            ></textarea>
          </div>
        </div>
        <div class="button-wrapper d-flex">
          <button class="btn btn-primary me-2" @click="saveTask">Save</button>
          <button class="btn btn-outline-secondary" @click="toggleCreating">
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
let tasks = ref([]);
const isCreating = ref(false);
let title = ref("");
let description = ref("");

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};
const toggleCreating = () => {
  isCreating.value = !isCreating.value;
};
const saveTask = () => {
  tasks.value.push({
    title: title.value,
    description: description.value,
    isDone: false,
  });
  toggleCreating();
  title = ref("");
  description = ref("");
};
const toggleTaskStatus = (task) => {
  task.isDone = !task.isDone;
};
</script>
<style>
.checked {
  text-decoration: line-through;
}
</style>
