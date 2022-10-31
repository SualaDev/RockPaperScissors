<template>
  <div class="container">
    <Header :score="score" />
    <GameSection @updateScore="onScoreUpdate" />
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      score: 0
    }
  },
  methods: {
    onScoreUpdate (score) {
      this.score = score
    }
  }
}
</script>
<style scoped>
.container{
  background: radial-gradient(circle, #1f3756 50%, #141539);
  min-height: 100vh;
  position: relative;
  max-width: 1400px;
  margin: 0 auto;
}
</style>