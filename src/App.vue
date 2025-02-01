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

}
</script>

<style>
.continer{
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
}

</style>
