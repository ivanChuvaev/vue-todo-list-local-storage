<script setup>
const emit = defineEmits(['add-task']);
const handleSubmit = (e) => {
  e.preventDefault();
  const data = Object.fromEntries(new FormData(e.target));
  e.target.reset();
  emit('add-task', data);
}
</script>

<template>
  <form class="flex flex-col gap-2 my-2 w-[300px]" @submit="handleSubmit">
    <input name="title" class="block border p-2 rounded" placeholder="Title" />
    <textarea name="description" class="block border p-2 rounded" placeholder="Description" rows="3" />
    <button class="block border p-2 rounded hover:bg-slate-50">Add task</button>
  </form>
</template>
