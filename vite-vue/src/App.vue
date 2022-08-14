<template>
  <StartGameComponent v-if="currentScreenStatus === screenStatus[0]" @onChooseLevel="handleBeforeStartGame($event)" />
  <MainGameComponent v-if="currentScreenStatus === screenStatus[1]" :widthProp="widthProp"
    @onFinishGame="handleGetResult()" :cardsContext="settings.cardsContext" />
  <EndGameComponent v-if="currentScreenStatus === screenStatus[2]" @onStartAgain="handleStartAgain()" :timer="timer" />

</template>
<script>
import StartGameComponent from './components/StartGameComponent.vue'
import MainGameComponent from './components/MainGameComponent.vue'
import EndGameComponent from './components/EndGameComponent.vue'

//utils 
import { shuffled } from './utils/array'

export default {
  name: "App",
  components: {
    StartGameComponent,
    MainGameComponent,
    EndGameComponent,
  },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: new Date().getTime(),
      },
      screenStatus: ['start', 'main', 'end',],
      currentScreenStatus: 'start',
      timer: 0,
      widthProp: 0,
    }
  },
  methods: {
    handleBeforeStartGame(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks
      if (config.totalOfBlocks === 16) {
        this.widthProp = 424
      }
      if (config.totalOfBlocks === 36) {
        this.widthProp = 666
      } if (config.totalOfBlocks === 64) {
        this.widthProp = 674
      }
      if (config.totalOfBlocks === 100) {
        this.widthProp = 682
      }

      const firstCards = Array.from({ length: this.settings.totalOfBlocks / 2 }, (_, i) => i + 1)
      const secondCards = [...firstCards]
      const totalCards = [...firstCards, ...secondCards]
      const totalCardsShuffle = shuffled(shuffled(totalCards))

      this.settings.cardsContext = totalCardsShuffle
      this.settings.startedAt = new Date().getTime()

      // data ready
      this.currentScreenStatus = this.screenStatus[1]

    },
    handleGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt


      this.currentScreenStatus = this.screenStatus[2]
    },
    handleStartAgain() {
      this.currentScreenStatus = this.screenStatus[0]

    }
  },
  async created() {

  }
}
</script> 
