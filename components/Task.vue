<script setup>
  const props = defineProps(['task'])
  const emit = defineEmits(['save'])
  const isEditing = ref(false);
  const title = ref(props.task.title);
  const description = ref(props.task.description);
  const save = () => {
    emit('save', { id: props.task.id, title: title.value, description: description.value });
    isEditing.value = false;
  }
</script>

<template>
  <div class="my-2 flex justify-between items-center shadow bg-white rounded py-2 px-5">
    <div v-if="!isEditing">
      <div class="font-bold text-lg">
        {{ task.title }}
      </div>
      <div>
        {{ task.description }}
      </div>
    </div>
    <div v-if="isEditing" class="w-1/2 flex flex-col gap-2">
      <input class="w-full border border-solid border-slate-300 px-2 rounded font-bold text-lg" name="title" placeholder="Title" v-model="title" />
      <textarea class="w-full border border-solid border-slate-300 px-2 rounded" rows="3" name="description" placeholder="Description" v-model="description" />
    </div>
    <div class="flex gap-2">
      <button class="shadow px-2 py-1 rounded hover:bg-blue-400 transition-colors duration-200" v-if="isEditing" @click="save">Save</button>
      <button class="shadow px-2 py-1 rounded hover:bg-blue-400 transition-colors duration-200" v-if="!isEditing" @click="isEditing = true">Edit</button>
      <v-icon name="fa-flang" />
      <button class="shadow px-2 py-1 rounded hover:bg-red-400 transition-colors duration-200" @click="$emit('delete', task.id)">Delete</button>
    </div>
  </div>
</template>
