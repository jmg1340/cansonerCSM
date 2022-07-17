<template>
  <div :class="{classFonsClar: !opcions.temaFosc,
                classFonsFosc: opcions.temaFosc}">

    <!-- <h1>{{ canso.titol}} </h1> -->

    <paragraf 
      v-for="(objP, index) in canso.lletra" 
      :key="index"
      :objP = "objP"
      :style="{ 'fontSize': opcions.tamanyLletra + 'px'}"
      class="pb-3 pt-3"

      :class="{classTornadaTemaClar: objP.tipus=='tornada' && !opcions.temaFosc,
                classTornadaTemaFosc: objP.tipus=='tornada' && opcions.temaFosc,
                classEstrofaTemaClar: objP.tipus=='estrofa' && !opcions.temaFosc,
                classEstrofaTemaFosc: objP.tipus=='estrofa' && opcions.temaFosc,
                classFonsClar: !opcions.temaFosc,
                classFonsFosc: opcions.temaFosc}"


    />

    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

  </div>
  
</template>



<script setup>
  import { ref, onMounted, onUnmounted } from 'vue'

  import paragraf from "../components/paragraf.vue"
  import cansoner from "../cansoner/cansoner.json"
  import router from "../router/index.js"
  console.log("router:", router)


  const props = defineProps(['id'])
  const canso = ref(cansoner[props.id])


  const opcions = ref ({
    tamanyLletra: 20,
    temaFosc: false
  })

  const increment = () => { opcions.value.tamanyLletra++  }
  const decrement = () => { opcions.value.tamanyLletra--  }


  const funcEventTecles = (event) => {  
    console.log("router2:", router)

    switch( event.key ){
      case "N":
      case "n":
        router.push({ path: "/" });         
        break;

      case "F":
      case "f":
        opcions.value.temaFosc = !opcions.value.temaFosc;         
        break;

      case "I":
      case "i":
        console.log("I apretada")
        location.href = "#/canso/#inici";;         
        break;

      case "+":
        console.log("+ apretada")
        increment()
        console.log(opcions.value.tamanyLletra)
        break;

      case "-":
        console.log("- apretada")
        decrement()
        break;
    } 
  }

  onMounted(() => {
    if (localStorage.getItem("CansonerCSM_key_opcions"))
          opcions.value = JSON.parse(localStorage.getItem("CansonerCSM_key_opcions"));
          // opcions.value.tamanyLletra = parseInt( opcions.value.tamanyLletra)


    document.addEventListener("keydown", funcEventTecles)
  })
  
  onUnmounted(() => {
    // guardem les opcions
    localStorage.setItem( "CansonerCSM_key_opcions", JSON.stringify(opcions.value) )

    document.removeEventListener("keydown", funcEventTecles)
  })
 

</script>



<style>
  .classTornadaTemaClar{
    color: #c10015;
  }

  .classTornadaTemaFosc{
    color: #f8c75d;
  }

  .classEstrofaTemaClar{
    color: black;
  }

  .classEstrofaTemaFosc{
    color: white;
  }

  .classFonsClar{
    background-color: white;
  }

  .classFonsFosc{
    background-color: black;
  }

</style>