<template>
  <div class="center-screen">
    <div class="flex flex-col m-auto">
      <p class="text-xl bold">Enas El Mershati</p>
      <h1 class="text-7xl bold">Développeuse web</h1>

      <div class="flex gap-4 mt-10">
        <NuxtLink :to="`/projects`" class="big-btn">
          Voir mes projets
        </NuxtLink>
        <NuxtLink :to="`/presentation`" class="big-btn">
          Ma présentation
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
</script>

<style scoped>
.center-screen {
  position: absolute;
  top: 50%;
  left: 50%;
  margin-right: -50%;
  transform: translate(-50%, -50%);
}
</style>