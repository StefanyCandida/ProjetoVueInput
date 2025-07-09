<template>
  <header :class="headerClass">
    <h1> Estudos </h1>
      <button :class="buttonClass" @click="onClick()">
    {{title}}
  </button>
  </header>

  <main>
   <div :class="wrapperClass">
      <HelloWorld   />
    </div>
  </main>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue' 
   const title= ref('Inverse')
    const isActive= ref(false) 
    const onClick = () => {
      console.log(isActive.value) 
   
       isActive.value = !isActive.value
   if(!isActive.value){
    title.value= "Inverse"
   } 
   if(isActive.value){
     title.value= "Normal"
   }
      
    }
  
  const buttonClass= computed(() => ({
        'btn': true,
        'inversebtn':isActive.value,

      }))
        const wrapperClass= computed(() => ({
        'wrapper': true,
        'wrapperinverse':isActive.value,

      }))
          const headerClass= computed(() => ({
        'wrapperheader': true,
        'wrapperheaderrinverse':isActive.value,

      }))
</script>



<style scoped>
  .wrapperheader {
    display: flex;
   flex-direction: column;
  }
  .wrapperheaderrinverse {
    display: flex; 
    background-color: black;
    place-items: flex-start;
    flex-wrap: wrap;    
      color: white;  
  }

    .wrapper {
    display: flex; 
    background-color: white;
    place-items: flex-start;
    flex-wrap: wrap;
    
  }
    .wrapperinverse {
    display: flex; 
    background-color: black;
    place-items: flex-start;
    flex-wrap: wrap;
    
  }
 
.btn {
  width: 50px;
  height: 30px;
  border-radius: 5px;
  border: 1px solid white; 
  background-color: black;
  display: flex;
  justify-content: center;
  align-items: center;
    color: beige;
  }
.inversebtn {
   background-color: white;
    border: 1px solid black; 
  color: black; 
  }

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
     background-color: black;
  }

  
    .wrapper {
    display: flex; 
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
