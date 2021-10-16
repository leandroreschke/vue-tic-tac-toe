<template>
  <div id="app" class="p-3">
    <div class="row mb-1">
      <div class="col items-center">
        <div class="fs-7" >Tic Tac Toe (VueJS 3.2)</div>
        <span class="fs-3">* This website use the theme from your computer / mobile (Light / Dark)</span>
      </div>
    </div>
    <div class="row self-center mb-1">
      <div class="col">
        <div class="status fs-5" >{{status}} {{ winner == '' ?  currentPlayer: winner}}</div>
      </div>
    </div>
    <div class="row self-center mb-1">
      <div class="col">
        <Button classes="success fs-4" :click="reset" >Reset</button>
      </div>
    </div>
    <div class="row content-center">
      <div class="col max-3">
        <div v-for="(row, outerI) in 3" class="row content-center" :key="row">
          <div class="col slotColumn" v-for="(button, innerI) in 3" :key="row+'_'+button">
            <Button classes="min slot " :click="() => place(outerI, innerI)">{{board[outerI][innerI]}}</Button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue';
  import Button from '../components/shared/Button.vue';
  /*I've never done a game with Vue, last time I did a game with only programming 
  was on my first year in college, C and commandline*/

  const winner = ref('') //Who won
  const status = ref('Next player: ') //Nice messages for the players
  const currentPlayer = ref('X') //shows current player
  const board = ref([['', '', ''], ['', '', ''], ['', '', '']]) //board representation
  

  //Resets the game
  const reset = () => {
    board.value.forEach(row => {
      row.forEach((col, index) => row.splice(index, 1, ''))
    })
    winner.value = ''
    status.value = 'Next player: '
    currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X'
  }
  
  //Place the current player into a slot. Also checks for a winner after that, and change the current player
  const place = (row, col) => {
    if(winner.value === ''){
      if(board.value[row][col] === ''){
        board.value[row].splice(col, 1, currentPlayer.value)
        checkWinner(row, col)
        if(winner.value === ''){
          currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X'
        }
      }
    }
  }
  /*That was difficult, first time I had 5 for loops, than I realized it could be better, 
  probably can be even better but I will stick with it.
  
  Search for a possible winners after a move(row, col, diag, reverse diag, draw)
  */
  const checkWinner = (rowP, colP) => {
    let slots = 3
    let row, col;
    for(let i = 0; i < 5; i++){
      if(winner.value !== ''){
        break;
      }else{
        for(let j = 0; j < slots; j++){
          switch(i){
            case 0:
              row = j
              col = colP
              break;
            case 1:
              row = rowP
              col = j
              break;
            case 2:
              row = j
              col = j
              break;
            case 3:
              row = j
              col = (slots-1) - j
              break;
            case 4:
              let draw = true;
              board.value.forEach(row => {
                if(draw){draw = !row.includes('')}
              })
              
              if(draw){
                status.value = 'Game Result: '
                winner.value = 'Draw'
              }
              break;
          }
          if(board.value[row][col] != currentPlayer.value || winner.value !== ''){
            break;
          }
          if(j === slots - 1){
            status.value = 'The Winner is: '
            winner.value = currentPlayer.value
          }
        }
      } 
    }
  }
    

</script>

<style scoped>

  .slotColumn {
    padding: .5rem;
  }

  .slot {
    aspect-ratio: 1 / 1;
    max-width: 1px;
    font-size: 4.0rem;
  }

  @supports not (aspect-ratio: 1 / 1) {
    .slot::before {
      float: left;
      padding-top: 100%;
      content: "";
    }

    .slot::after {
      display: block;
      content: "";
      clear: both;
    }
  }


</style>