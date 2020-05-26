<template>
<div>
    <players></players>
    <starter v-if="!gameOn" @start="start"></starter>
    <game v-if="gameOn" @win="win" @lose="lose"></game>
</div>
</template>

<script>
import {eventBus} from './main';
import players from './components/players';
import starter from './components/starter';
import game from './components/game'

export default {
  data(){
    return {
      gameOn : false
    };
  },
  methods : {
    start(){
      this.gameOn = true;
    },
    win(health){
      this.gameOn = false;
      alert(`You Have Defeated The Monster With Your Health ${health}`)
      eventBus.$emit('reset');
    },
    lose(health){
      this.gameOn = false;
      alert(`You Have Been Defeated And The Monster Health Is ${health}`)
      eventBus.$emit('reset');
    }
  },
  components : {
    players,
    starter,
    game
  }
}
</script>

<style>
  .text-center {
    text-align: center;
  }

  .controls, .log {
    margin-top: 30px;
    text-align: center;
    padding: 10px;
    border: 1px solid #ccc;
    box-shadow: 0px 3px 6px #ccc;
  }

  .turn {
    margin-top: 20px;
    margin-bottom: 20px;
    font-weight: bold;
    font-size: 22px;
  }

  .log ul {
    list-style: none;
    font-weight: bold;
    text-transform: uppercase;
  }

  .log ul li {
    margin: 5px;
  }

  .log ul .player-turn {
    color: blue;
    background-color: #e4e8ff;
  }

  .log ul .monster-turn {
    color: red;
    background-color: #ffc0c1;
  }

  button {
    font-size: 20px;
    background-color: #eee;
    padding: 12px;
    box-shadow: 0 1px 1px black;
    margin: 10px;
  }
</style>