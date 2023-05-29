<template>
  <main-component
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-component
    v-if="statusMatch === 'interact'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  />
  <result-component
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
  <p class="copyright">
    Mini Project created by thangvd2312 - Vue
    <a
      href="https://github.com/thangvd2312/vue3-for-beginners/tree/main/pokemon-memory"
      >View here</a
    >
  </p>
</template>

<script>
import MainComponent from "./components/Main.vue";
import InteractComponent from "./components/Interact.vue";
import ResultComponent from "./components/Result.vue";
import { shuffled } from "./utils/array";

export default {
  name: "App",
  components: {
    MainComponent,
    InteractComponent,
    ResultComponent,
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
  methods: {
    onHandleBeforeStart(configs) {
      this.settings.totalOfBlocks = configs.totalOfBlocks;

      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];

      this.settings.cardsContext = shuffled(shuffled(shuffled(cards)));
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "interact";
    },
    onGetResult() {
      this.statusMatch = "result";
      this.timer = new Date().getTime() - this.settings.startedAt;
    },
  },
};
</script>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 0;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
