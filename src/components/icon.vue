<template>
  <div :class="iconClass" @click=clickicon($event)  >       
   
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';
const props = defineProps<{
  selected: boolean
}>();
const isSelected= ref(props.selected) 

  const clickicon = (item : any) => {
    isSelected.value = !isSelected.value;
  emit(clickicon,item)
       console.log(item)
    }


const iconClass = computed(() => ({
  icon: true,
  selected: isSelected.value,
}));


function emit(clickicon: (item: any) => void, item: any) {
    throw new Error('Function not implemented.');
}
</script>

<style scoped>
.icon {
width: 10px;
height: 10px;
border: solid 1px;
}
.icon:hover{
    background-color: azure;
}
.icon.selected{
 border: white solid 1px; 
  background-color: azure;  
}


</style>