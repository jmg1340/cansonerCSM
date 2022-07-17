<template>
    <div class="card" :class="{ csstornada: objP.tipus == 'tornada' }">
      <div
        v-for="(linia, index) in objP.paragraf"
        :key = "'L'+index"
      >
          {{ linia }}
      </div>
    </div>
</template>

<script setup>
  const props = defineProps(['objP'])
  console.log("OBJP", props.objP)

  

</script>

<style>
  .csstornada {
    color: rgb(200, 0, 0)
  }

</style>