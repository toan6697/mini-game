<template>
  <div id="app">
    <div class="wrapper clearfix">
            
            <Players 
            v-bind:scorePlayer="scorePlayer" 
            v-bind:currentScore="currentScore"
            v-bind:activePlayer="activePlayer"
            >
            </Players>

            <Controls v-bind:isPlaying="isPlaying"
                      v-on:startGame="startGame()"
                       v-on:handleRollDice="handleRollDice()" 
                       v-on:handleHoldScore="handleHoldScore()">
            </Controls>
            <Dices v-bind:dices="dices" ></Dices>
            
    </div>
    <Popup v-bind:isPlaying="isPlaying" v-on:confirm="confirm"></Popup>
  </div>
</template>

<script>
import Players from "./components/Players";
import Controls from "./components/Controls";
import Dices from "./components/Dices";
import Popup from "./components/Popup";

export default {
  name: 'app',
  data () {
    return {
       isPlaying : false,
       startGaming : false,
       scorePlayer : [13, 30],
       currentScore :30, // điểm hiện tại
       activePlayer :1, // xác định người chơi
       dices : [2, 2]  // số điểm trên xúc sắc sau khi gieo 
    }
  },
  components : {
    Players,
    Controls,
    Dices,
    Popup
  },
  methods: {
    startGame(){
        this.isPlaying = true;
    },
    confirm(){
        this.isPlaying = false;
        this.startGaming = true;
        this.scorePlayer = [0 , 0];
        this.currentScore = 0;
        this.activePlayer =0; 
        this.dices= [2, 2];
    },
    handleRollDice(){
        if(this.startGaming){
           let firstDice = Math.ceil(Math.random() * 6);
           let secondDice = Math.ceil(Math.random() * 6);
           
           //console.log(firstDice, secondDice);
           this.dices = [ firstDice, secondDice ];

           if(firstDice === 1 || secondDice === 1){
             var that = this;
             setTimeout( function(){
                 alert(`người chơi ${that.activePlayer +1} đã quay vào 1`);
             }, 10 )
             //alert('đổi lượt chơi'); // bị dừng ở đây do nó chờ hàm này chạy xong ms chạy tiếp xuống dưới
             firstDice = 0;
             secondDice = 0;
             
             //console.log(this.activePlayer);
               if(this.activePlayer  ===  0){
                 this.activePlayer = 1;
                 this.currentScore = 0;
                 let sum = firstDice + secondDice;
                 this.currentScore += sum;
                 return;
               }
               if(this.activePlayer === 1){
                 this.activePlayer = 0;
                 this.currentScore = 0;
                 let sum = firstDice + secondDice;
                 this.currentScore += sum;
                 return;
               }
           }else{
              let sum = firstDice + secondDice;
              this.currentScore += sum;
           }
        }
        else{
          alert('Vui lòng ấn new game để bắt đầu chơi');
        }
    },
    handleHoldScore(){
      if(this.startGaming){
         //this.activePlayer = this.activePlayer === 0 ? 0 : 1;
          this.scorePlayer[this.activePlayer] = this.scorePlayer[this.activePlayer] + this.currentScore;
          console.log(this.scorePlayer);
          
          this.activePlayer = this.activePlayer === 0 ? 1: 0;
          this.currentScore = 0;
          return;
      }else{
         alert('Vui lòng ấn new game để bắt đầu chơi');
      }
    }
  }
}
</script>

<style>
/**********************************************
*** GENERAL
**********************************************/

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url("./assets/back.jpg");
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}

</style>
