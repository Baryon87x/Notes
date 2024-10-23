<template>
  <main class="w-full h-screen flex flex-col justify-center items-center">
    
    <button 
      class="p-2 px-4 bg-blue-600 hover:bg-blue-900 duration-200 ease-in-out rounded-sm text-white"
      @click="visible = true">
      Ajouter une observation 
    </button>



    <Dialog
      v-model:visible="visible"
      maximizable
      modal
      header="Ajouter une note"
      :style="{ width: '50rem' }"
      :breakpoints="{ '1199px': '75vw', '575px': '90vw' }"
    >
      <Editor v-model="wordValue" editorStyle="height: 320px" />
      <template #footer>
        <section class="w-full flex justify-end">
          <div class="space-x-4">
            <button
              class="p-1 px-3 rounded-sm bg-yellow-500 hover:bg-yellow-600 text-white"
              v-show="wordValue.length>0"
              @click="valider"
            >
              valider
            </button>
          </div>
        </section>
      </template>
    </Dialog>

    <ListeNotes :ListesNote="ListesNote" class="mt-5"/>
  </main>
</template>
<script setup lang="ts">
import Editor from "primevue/editor";
import Button from "primevue/button";
import Dialog from "primevue/dialog";
import ListeNotes from '@/components/ListeNotes.vue'
import { ref,reactive } from "vue";

interface ListeNote {
  content?: string,
}
const wordValue = ref<string>('');
const visible = ref(false);
const id = ref<number>(1)
const ListesNote: ListeNote[] = reactive([]); 

const annuler = () => (wordValue.value = "");

const valider = () => {
  ListesNote.push({id:id.value++ ,content:wordValue.value});
  visible.value = !visible.value;
  
}
</script>
