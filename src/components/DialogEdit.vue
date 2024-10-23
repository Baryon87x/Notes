<template>
  <Dialog 
    v-model:visible="visible" 
    modal 
    :header="`note ${props.item.id}`" 
    :style="{ width: '50vw' }" 
    :breakpoints="{ '1199px': '75vw', '575px': '90vw' }">
    <p class="m-0" v-html="props.item.content"></p>
  </Dialog>
</template>
<script setup lang="ts">

import Dialog from 'primevue/dialog';

interface Item {
  id: number;
  content: string;
}
interface Props{
  visible: boolean;
  item:Item;
}
const props = defineProps<Props>();
const visible = ref(props.visible);


</script>