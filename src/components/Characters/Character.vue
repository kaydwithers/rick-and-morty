<template>
  <li class="character">
    <a href="">
      <p>{{ character.name }}</p>
    </a>
  </li>
</template>

<script>
export default {
  props: ["character"],
};
</script>

<style scoped>
.character {
  background-color: #fff;
  list-style: none;
  width: 100%;
}

.character a {
  display: block;
  padding: 2rem;
}

@media (min-width: 768px) {
  .character {
    width: 25%;
  }
}
</style>
