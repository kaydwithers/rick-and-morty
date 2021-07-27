<template>
  <div class="modal">
    <div class="modal__overlay" />

    <div class="modal__content">
      <h1>Modal</h1>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  display: flex;
  height: 100%;
  align-items: center;
  justify-content: center;
  left: 0;
  top: 0;
  width: 100%;
}

.modal__overlay {
  position: absolute;
  background-color: #1a202c;
  height: 100%;
  left: 0;
  opacity: 0.5;
  width: 100%;
}

.modal__content {
  background-color: #fff;
  height: 50%;
  margin: 4rem;
  padding: 4rem;
  width: 100%;
  z-index: 1;
}
</style>
