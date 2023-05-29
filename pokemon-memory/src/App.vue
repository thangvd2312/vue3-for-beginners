<template>
  <main-component
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-component v-if="statusMatch === 'interact'" />
  <footer-component />
</template>

<script>
import FooterComponent from "./components/Footer.vue";
import MainComponent from "./components/Main.vue";
import InteractComponent from "./components/Interact.vue";
export default {
  name: "App",
  components: {
    MainComponent,
    FooterComponent,
    InteractComponent,
  },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      timer: 0,
      statusMatch: "default",
    };
  },
};
</script>

<style lang="css" scoped></style>
