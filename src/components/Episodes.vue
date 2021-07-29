<template>
  <Button @click="handleAccordion">
    Episodes <span v-if="isExpanded">⬆</span><span v-else>⬇</span>
  </Button>

  <transition name="fade">
    <div v-show="isExpanded">
      <p>Episodes: {{ character.episode.length }}</p>
    </div>
  </transition>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Episodes",
  components: {
    Button,
  },
  data() {
    return {
      isExpanded: false,
    };
  },
  methods: {
    /**
     * Handle the click of the dropdown button.
     */
    handleAccordion() {
      this.isExpanded = !this.isExpanded;
    },
  },
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
