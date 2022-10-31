<template>
  <div class="container">
    <div v-if="userPick.length === 0">
      <div class="top_image">
        <img class="paper" :src="require(`assets/images/${images[0]}`)" alt="" @click="play('paper', 0)" />
        <img class="scissors" :src="require(`assets/images/${images[1]}`)" alt="" @click="play('scissors', 1)" />
      </div>
      <div class="bottom_image">
        <img class="rock" :src="require(`assets/images/${images[2]}`)" alt="" @click="play('rock', 2)" />
      </div>
    </div>
    <div v-else class="top_image">
      <div class="user-input">
        <img :src="require(`assets/images/${userImage}`)" class="userpick" :class="userPick" alt="" />
      </div>
      <div class="result-container">
        <div class="game-result">
          {{ result }}
        </div>
        <div>
          <button class="repeat" @click="userPick = ''">Play Again</button>
        </div>
      </div>
      <div>
        <div v-if="loading" class="loading-dot"></div>
        <div v-else class="computer-input">
          <img :src="require(`assets/images/${imageDisplay}`)" :class="{ 'paper': imageDisplay === images[0], 'scissors': imageDisplay === images[1], 'rock': imageDisplay === images[2] }" alt="" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name:"GameSection",
    data() {
      return {
        loading: false,
        result: '',
        userPick: '',
        images: [
          'icon-paper.svg',
          'icon-scissors.svg',
          'icon-rock.svg'
        ],
        userImage: '',
        score: 0,
        imageDisplay: ''
      }
    },
    watch: {
      userPick () {
        this.result = ''
      }
    },
    methods: {
      play(input, imageIndex) {
        this.userPick = input
        this.userImage = this.images[imageIndex]
        this.calculateWinner()
        this.calcuateGame()
     },
      calculateWinner () {
        this.loading = true
        setTimeout(() => {
          this.loading = false
          if (this.userPick === 'rock' && this.imageDisplay.includes('paper')) {
            this.result = 'You Lose'
          } else if (this.userPick === 'rock' && this.imageDisplay.includes('scissors') ) {
            this.result = 'You Win'
          } else if (this.userPick === 'paper' && this.imageDisplay.includes('scissors') ) {
            this.result = 'You Lose'
          } else if (this.userPick === 'paper' && this.imageDisplay.includes('rock') ) {
            this.result = 'You Win'
          } else if (this.userPick === 'scissors' && this.imageDisplay.includes('rock') ) {
            this.result = 'You Lose'
          } else if (this.userPick === 'scissors' && this.imageDisplay.includes('paper') ) {
            this.result = 'You Win'
          } else if (this.userPick === 'scissors' && this.imageDisplay.includes('scissors') ) {
            this.result = 'You Draw'
          } else if (this.userPick === 'paper' && this.imageDisplay.includes('paper') ) {
            this.result = 'You Draw'
          } else if (this.userPick === 'rock' && this.imageDisplay.includes('rock') ) {
            this.result = 'You Draw'
          } 
          if (this.result === 'You Lose') {
            --this.score
          } else if (this.result === 'You Win') {
            ++this.score
          }
          this.$emit('updateScore', this.score)
        }, 3000)
      },
      calcuateGame(){
        const newArray = [0,1,2]
        const randomSelection = newArray[Math.floor(Math.random()*newArray.length)] 
        this.imageDisplay= this.images[randomSelection]
      }
    }
  }     
</script>

<style scoped>
.container{
  position: relative;
}
.top_image {
  width: 35%;
  margin: 50px auto;
  display: flex;
  justify-content: space-between;
}
.bottom_image {
  /* width: 30%; */
  margin: auto;
  display: flex;
  padding-top: 2rem;
  justify-content: center;
}
.paper{
  background-color: #FFF;
  padding: 1.2rem;
  border: 12px solid #4865f4;
  border-radius: 50%;
  cursor: pointer;
}
.scissors{
  background-color: #FFF;
  padding: 1.2rem;
  border: 12px solid #ec9e0e;
  border-radius: 50%;
  cursor: pointer;
}
.rock{
  background-color: #FFF;
  padding: 1.2rem;
  border: 12px solid #dc2e4e;
  border-radius: 50%;
  cursor: pointer;
}
.repeat{
  background-color: white;
  color: #2a46c0;
  border-radius: 8px;
  padding: 3.1% 15%;
  font-size: 1.5rem;
  cursor: pointer;
}
.result-container{
  display: flex;
  flex-direction: column;
  row-gap: .5rem;
}
.game-result{
  color: #FFF;
  font-size: 2.75rem;
  margin-top: 1rem;
}
.computer-image{
  border: none;
  border-radius: 50%;
  width: 45%;
  height: 45%;
  animation: pulse-animation 1.5s ease-out infinite;
  background-color: red;
}
.loading-dot {
  border-radius: 50%;
  border: 1px solid #000;
  width: 7rem;
  height: 7rem;
  background-color: rgba(0, 0, 0, 0.841);
  -ms-grid-row: 1;
  -ms-grid-column: 2;
  grid-area: houseSelection;
  -webkit-animation: pulse-animation 1.5s ease-out infinite;
          animation: pulse-animation 1.5s ease-out infinite;
}
@-webkit-keyframes pulse-animation {
  0% {
    -webkit-transform: scale(1);
            transform: scale(1);
  }
  50% {
    -webkit-transform: scale(1.5);
            transform: scale(1.5);
    opacity: 0.3;
  }
  100% {
    -webkit-transform: scale(1);
            transform: scale(1);
    opacity: 0.5;
  }
}
@keyframes pulse-animation {
  0% {
    -webkit-transform: scale(1);
            transform: scale(1);
  }
  50% {
    -webkit-transform: scale(1.5);
            transform: scale(1.5);
    opacity: 0.3;
  }
  100% {
    -webkit-transform: scale(1);
            transform: scale(1);
    opacity: 0.5;
  }
}
@media screen and (max-width: 1200px){
  .top_image{
    width: 42%;
  }
}
@media screen and (max-width: 1050px){
  .top_image{
    width: 50%
  }
}
@media screen and (max-width: 850px){
  .top_image{
    width: 58%;
  }
}
@media screen and (max-width: 700px){
  .top_image{
    width: 80%;
  }
}
@media screen and (max-width: 500px){
  .top_image{
    width: 90%;
  }
}
</style>