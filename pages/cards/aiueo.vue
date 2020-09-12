<template>
  <div
    class="w-screen h-screen flex items-center justify-center"
    @click="onClick"
  >
    <template v-if="phase === phases.READY">クリックして開始</template>
    <template v-else-if="phase === phases.PROGRESS"
      ><BaseCard v-if="currentCard" v-text="currentCard.text"
    /></template>
  </div>
</template>

<script>
import { hiraganaMora } from '~/constants/cardList'
const phases = {
  READY: 'READY',
  PROGRESS: 'PROGRESS',
}
export default {
  data() {
    return {
      phase: phases.READY,
      cardList: [...hiraganaMora],
      cardCount: 0,
    }
  },
  computed: {
    currentCard() {
      return this.cardList[this.cardCount]
    },
    phases() {
      return phases
    },
  },
  methods: {
    onClick() {
      switch (this.phase) {
        case phases.READY:
          this.phase = phases.PROGRESS
          break
        case phases.PROGRESS:
          if (this.cardCount + 1 >= this.cardList.length) {
            this.cardCount = 1
            this.phase = phases.READY
          } else {
            this.cardCount++
          }
          break
      }
    },
  },
}
</script>

<style lang="scss" scoped></style>
