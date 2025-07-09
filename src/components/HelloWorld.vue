<template>
   
  <div :class="divClass">
  
  <input class="input" v-model="inputValue" placeholder="Placeholder"  @click="onClickInput($event)" @focus="onFocus"
      @blur="onBlur"/>

        <div class="list-container">
            <template v-for="(item, index) in filteredItems" :key="index">    
           <Floating
    :item="item.item"
    :value="item.value"
    :selected="selectedItems.includes(item.item)"
    @click="onClickItem($event)"
  />
 
</template>
        </div>
  </div>
  

</template>
<script setup lang="ts">
import { computed,  ref, watch } from 'vue';
 import Floating from './Floating.vue' 

const isActive= ref(false) 
const isFocus = ref(false);

const inputValue = ref('');
const render = [
  { item: 'Ana', value: 1 },
  { item: 'Perola', value: 2 },
  { item: 'Carol', value: 3 },
  { item: 'Daniele', value: 4 },
  { item: 'Laura', value: 5 },
  { item: 'Fernanda', value: 6 },
  { item: 'Maria', value: 7 },
  { item: 'Luisa', value: 8 },  
  { item: 'Julia', value: 9 },
  { item: 'Helena',  value: 10 },
  { item: 'Geovana', value: 11 },
  { item: 'Larissa', value: 12 },
];
 
     const onClickInput = (item : any) => {
      console.log(item, '56')
     
    }
  const selectedItems = ref<string[]>([]);

const onClickItem = (item: string) => {
  if (selectedItems.value.includes(item)) {
    selectedItems.value = selectedItems.value.filter((i) => i !== item);
  } else {
    selectedItems.value.push(item);
  }
};
const onFocus = () => {
  isFocus.value = true;
  console.log('Com foco', isFocus.value);
};

const onBlur = () => {
  isFocus.value = false;
  console.log('Sem foco:', isFocus.value);
};
  
    
       const divClass= computed(() => ({
        'div': true,
        'inverse':isActive.value,

      }))
 const filteredItems = computed(() => {
  const normalizedInput = inputValue.value
    .toLowerCase()
    .normalize('NFD')  
    .replace(/[\u0300-\u036f]/g, '').trim();

  return render.filter((obj) =>
    obj.item
      .toLowerCase()
      .normalize('NFD')
      .replace(/[\u0300-\u036f]/g, '')
      .includes(normalizedInput)
  );
});
 watch(inputValue, (newValue) => {
  console.log( newValue);})
</script>

 

<style scoped>
.div {

  display: flex; 
  flex-direction: column;
  padding:   10px  ;
}
  .inverse {
    background-color: pink;
  }

.list-container {
  max-height: 200px; 
  overflow-y:scroll;
 
  scrollbar-width:initial; 
}
.list-container::-webkit-scrollbar {
  width: 3px;  
}

.list-container::-webkit-scrollbar-thumb {
 
  border-radius: 1px 1px  1px 0 ;  
}

.list-container::-webkit-scrollbar-thumb:hover {
  background-color: #555; 
}

.input {
    width: 230px;   
  color: rgb(96, 98, 114);
  border: 1px solid white;
  border-bottom: 1px solid black;
  border-radius:   3px 3px 0 0;
  padding: 0 0 0 10px  ;
  height: 30px;
}
.input:focus {
  outline: none; 
}
</style>

