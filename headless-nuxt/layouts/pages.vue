<template>
    <main role="">
        <div class="bg-index text-white min-h-screen">
            <slot />
        </div>
    </main>
</template>
  

<style scoped>
.bg-index {
    background: rgb(121, 9, 100);
    background: linear-gradient(180deg,
            rgba(121, 9, 100, 1) 0%,
            rgba(5, 25, 55, 1) 90%);
}
</style>