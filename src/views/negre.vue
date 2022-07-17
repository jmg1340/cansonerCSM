<template >
  <div class=" cssNegre">
    {{ inputNumero}}
  </div> 
</template>

<script setup>
  import { ref, onMounted, onUnmounted } from 'vue'
  import router from "../router/index.js"
  import cansoner from "../cansoner/cansoner.json"

  let inputNumero = ref("")

  onMounted(() => {
    document.addEventListener("keydown", funcEventTecles)
  })
  
  onUnmounted(() => {
    document.removeEventListener("keydown", funcEventTecles)
  })
  

  const funcEventTecles = function(event){
    
    switch( event.key ){

      case "N":
      case "n":
        router.back();
        break;

      case "VK_DELETE":   //windows
      case "kVK_ForwardDelete":  // MAC        
      case "Delete":
        inputNumero.value = "";
        break;

      case "VK_RETURN":   //windows
      case "kVK_Return":  // MAC
      case "Enter":
        mostrarCansoNumero();
        break;

      default:
        if (inputNumero.value.length < 3 && !isNaN(event.key)) inputNumero.value = inputNumero.value.concat(event.key);
        // this.inputNumero += event.key;
        console.log(`tecla ${event.key}`)
        break;

    } 
  }


  const mostrarCansoNumero = () => { 
    if ( cansoner[inputNumero.value] != undefined) {
      router.push( {path: "/canso/" + inputNumero.value})
    } else {
      inputNumero.value = "No existeix"
    }
    
  }



</script>

<style>
  .cssNegre {
    width: 100vw;
    height: 100vh;
    background: black;
  }

</style>