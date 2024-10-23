<template>
  
  <div v-if="notes.length > 0" class="w-2/4">
    <ul class="flex flex-col">
      <li class="my-2 p-4 rounded-md bg-slate-500 hover:shadow-xl duration-500 ease-in-out" v-for="item in notes" :key="item.id">
        <div class="w-full flex justify-between items-center">
          <p>Note {{ item.id }}</p>
          <div class="ms-4 flex space-x-2">
            <Dialog :visible="visible" :item="item"/>
            <button 
            @click="visible=!visible"
            class="bg-yellow-400 w-24 h-8 text-sm font-bold text-white rounded-sm">
              Voir <i class="pi pi-eye"></i>
            </button>
            <button 
              class="w-28 h-8 bg-red-400 text-sm font-bold text-white rounded-sm"
              @click="deleteItem(item.id)"
            >
              Supprimer <i class="pi pi-trash"></i>
            </button>
          </div>
        </div>
      </li> 
    </ul>
  </div>

  <div v-else class="w-2/4 h-32 flex items-center justify-center rounded-md bg-gray-700">
    <p class="text-white">Vous n'avez pas entré de note :(</p>
  </div>
</template>

<script setup lang="ts">
import { ref,watch } from 'vue';
import Dialog from '@/components/DialogEdit.vue'

interface Note {
  id?: number;
  content?: string;
}

interface Props {
  ListesNote: Note[];
}

const props = defineProps<Props>();
const notes = ref<Note[]>([...props.ListesNote]);
const visible = ref(false);

console.log(props);



const deleteItem = (id: number) => {
  notes.value = notes.value.filter(data => data.id !== id);
};
</script>
