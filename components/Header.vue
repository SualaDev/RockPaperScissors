<template>
  <div class="main-container">
    <div class="sub-container">
      <div class="inner-container">
        <h2 class="header-title"><img src="~assets/images/logo.svg" alt=""></h2>
        <div class="header-score">
          <h1 class="score">Score</h1>
          <h2 class="number">{{ score }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name:"HeaderPage",
    props: {
      score: {
        type: Number,
        default: 0
      }
    }
  }
</script>

<style scoped>
.main-container{
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 3rem;
  padding-bottom: 3rem;
}
.header-title{
  color: #FFF;
  text-transform: uppercase;
  font-size: 20px;
}
.sub-container{
  /* width: 400px; */
  border: 1px solid grey;
  border-radius: 8px;
}
.inner-container{
  padding: 1.5rem;
  display: flex;
  column-gap: 22rem;
}
.header-score{
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  background-color: #f0f2f4;
  padding: 1.2rem;
  border-radius: 8px;
  text-align: center;
}
.score{
  color: #2a46c0;
  font-size: 1rem;
  text-transform: uppercase;
}
.number{
  color: #3b4363;
  font-weight: 700;
  font-size: 1.5rem;
}
@media screen and (max-width: 700px){
  .inner-container{
    display: flex;
    column-gap: 13rem;
  }
}
@media screen and (max-width: 500px){
  .inner-container{
    display: flex;
    column-gap: 8rem;
  }
}
</style>