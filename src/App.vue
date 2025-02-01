<template>
  <div class="continer">
    <h1>xo game</h1>
    <div class="borad">
      <div v-for="(cell , index ) in board" :key="index" class="cell" @click="makemove(index)">

        {{ cell }}
      </div>
<p class="massage">{{massage}}</p>
<button class="reset" @click="resetGame">شروع مجدد بازی</button>


    </div>



  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
    GameOver:false,
    currentplayer:'x',
    massage:'نوبت بازیکن x',
    board:Array(9).fill(''),
  }
},
methods:{
  makemove(index){
    if(this.board[index] ==='' && !this.GameOver){
      this.board[index]=this.currentplayer
      if(this.checkWinner){
        this.massage=` برنده شد بازیکن ${this.currentplayer}`;
        this.GameOver=true;
      }
      if(!this.board.includes('')){
        this.massage= `بازی مساوی شد `;
        this.GameOver=true;
      }
      this.currentplayer=this.currentplayer==='x'?'o' : 'x'
      this.massage= ` نوبت بازیکن ${this.currentplayer}`
    }
  },
  checkWinner(){
    const winpatterns = [
      [0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]
    ]
    return winpatterns.some(patterns =>{
      const [a,b,c] = patterns
      return this.board[a] && this.board[a]===this.board[b] && this.board[a] === this.board[c]
    })
  },
  resetGame(){
    this.GameOver=false,
    this.currentplayer='x',
    this.massage='نوبت بازیکن x',
    this.board=Array(9).fill('')
  }
}

}
</script>

<style>
.continer{
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
}

</style>
