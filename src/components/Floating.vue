<template>
  <div :class="divClass" @click="onClickItem">   
      
    <div class="icontext"> 
      <Floating :selected="isSelected" @clickicon="onClickItem"/>
      <span class="paragrafo">
      {{ item }}
    </span>     
    </div>
  
     <Floating :selected="isSelected" />
   
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';
import Floating from './icon.vue'
const props = defineProps<{
  item: string
  value: number
}>();

const emit = defineEmits<{
  (e: "onClickItem", value: string): void
}>();


const isSelected = ref(false);

const divClass = computed(() => ({
  floating: true,
  selected: isSelected.value,
}));

const onClickItem = () => {
  isSelected.value = !isSelected.value;
  
  emit('onClickItem', props.item);
};


</script>

<style scoped>
.floating {
  width: 230px;
  height: 30px;
  background-color: white;
  padding: 10px;
  border: 1px  solid grey;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
}
.floating:not(:last-child) {
  border-bottom: none;
}
.floating:last-child {
  border: 1px  solid grey;
  border-radius:  0 0  3px 3px;
}
.floating:hover {
  background-color: rgb(91, 160, 216);
}

.floating.selected {
  background-color: rgb(31, 31, 173);
 
.paragrafo {
   color: white;
   padding: 5px;
}
}
.paragrafo {
   color: black;
   padding: 5px;
}
.icontext {
  width: 200px; 
  display: flex;
  align-items: center;
}

</style>