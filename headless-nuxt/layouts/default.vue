<template>
  <main role="">
    <div class="bg-index text-white min-h-screen">
      <slot />
      <div class="footer flex gap-2">
        <a href="https://github.com/enas-elm" target="_blank">
          <img src="@/assets/img/github.svg" alt="" />
        </a>
        <a href="https://www.linkedin.com/in/enas-el-mershati" target="_blank">
          <img src="@/assets/img/linkedin.svg" alt="" />
        </a>
      </div>
    </div>
  </main>
</template>

<style>
.bg-index {
  background: rgb(121, 9, 100);
  background: linear-gradient(180deg,
      rgba(121, 9, 100, 1) 0%,
      rgba(5, 25, 55, 1) 90%);
}

.footer {
  position: absolute;
  bottom: 0%;
  left: 50%;
  margin-right: -50%;
  transform: translate(-50%, -50%);
}
</style>