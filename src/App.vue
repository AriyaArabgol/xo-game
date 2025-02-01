<template>
  <div class="continer">
    <h1>xo game</h1>
    <div class="borad">
      <div v-for="(cell , index ) in board" :key="index" class="cell" @click="makemove(index)">
        {{ cell }}
      </div>
    </div>
    <p class="massage" > {{ massage }}</p>
      <button class="reset" @click="resetGame">Restart the game</button>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
    GameOver:false,
    currentplayer:'x',
    massage:`Player X's turn`,
    board:Array(9).fill(''),
  }
},
methods:{
  makemove(index){
    if(this.board[index] ==='' && !this.GameOver){
      this.board[index]=this.currentplayer;
      if(this.checkWinner()){
        this.massage=`🎉 Player ${this.currentplayer} wins! Congratulations!`;
        this.GameOver=true;
        return;
      }
      if(!this.board.includes('')){
        this.massage= `It's a draw!`
        this.GameOver=true;
        return;
      }
      this.currentplayer=this.currentplayer==='x'?'o':'x'
      this.massage= `Player ${this.currentplayer}'s turn`
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
    this.massage=`Player X's turn`,
    this.board=Array(9).fill('')
  }
}

}
</script>

<style>
*{
  background-color: rgb(0, 255, 255);
}
.continer{
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
}
.borad{
  display: grid;
  grid-template-columns: repeat(3,100px);
  grid-gap: 1px;
  margin-top: 20px;
  justify-content: center;

}
.cell{
  width: 100px;
  height: 100px;
  background-color: rgb(255, 240, 245)  ;
  display: flex;
  cursor: pointer;
  border: 2px solid black;
  justify-content: center;
  align-items: center;
  font-size: 30px;
  font-weight: bold;

}
.cell:hover{
  background-color: rgb(173, 216, 230);
}
.massage{
  font-weight: bold;
  font-size: 17px;
  margin-top: 19px;
  
}
.reset{
    padding: 15px;
    border: none;
    border-radius: 5px;
    background-color: rgb(18, 33, 167);
    font-size: 19px;
    cursor: pointer;
    color:white
}
.reset:hover{
    background-color: rgb(155, 7, 88);
}

</style>
