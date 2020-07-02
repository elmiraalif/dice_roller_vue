<template>
  <div>
    <!-- A dynamic heading where triggers the zomm-in-out animation, as soon as the dices are rolled and the result is out -->
    <h1 :class="{'zoom-in-out' : rolledDices}">{{heading}}</h1>

    <!-- This dice roller button only shows up when the game has not started yet(startGame === true): Just a boolean value to apply this effect -->
    <!-- When the game is not started yet, The text on the button is Roll Dices -->
    <button v-if="startGame" class="roller" @click="rollDice">
      <img src="../assets/dice-solid.svg" alt />
      <span>Roll Dices</span>
    </button>
    <!-- this is the else condition for the button, this one shows up when the game has been started and wants to refresh everything for a new game -->
    <button v-else class="roller" @click="reset">
      <img src="../assets/dice-solid.svg" alt />
      <span>New Game</span>
    </button>

    <div class="game-wrapper">
      <div>
        <div class="player one">
          <!-- We bind the src of the image , because it'll conditionally change 
          - also applying some animation using a library called animate.css as a try, this animation happens as soon as the dices get rolled-->
          <img
            :src="diceOneImagePath"
            alt
            :class="{'animate__animated animate__wobble': rolledDices}"
          />
        </div>
        <h2>Player 1</h2>
      </div>
      <div>
        <div class="player two">
          <!-- Same happens to the player 2 -->
          <img
            :src="diceTwoImagePath"
            alt
            :class="{'animate__animated animate__wobble': rolledDices}"
          />
        </div>
        <h2>Player 2</h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  //   This is where all the data regarding the game gets stored
  // We initialize them all and then change them through methods
  data() {
    return {
      diceOne: "",
      diceTwo: "",
      diceOneImagePath: "images/bet.svg",
      diceTwoImagePath: "images/bet.svg",
      heading: "Welcome to The Game!",
      rolledDices: false,
      startGame: true
    };
  },
  methods: {
    //   This method gets called when the button of Roll Dices gets clicked
    rollDice: function() {
      // Getting a random number between 1 - 6
      let diceOne = Math.floor(Math.random() * 6) + 1;
      let diceTwo = Math.floor(Math.random() * 6) + 1;
      //   We set them as the data properties outside methods
      this.diceOne = diceOne;
      this.diceTwo = diceTwo;

      this.diceOneImagePath = "images/" + diceOne + ".svg";
      this.diceTwoImagePath = "images/" + diceTwo + ".svg";
      //   Changing the booleans to change the conditions
      this.rolledDices = true;
      this.startGame = false;

      // An if statement for the result of the game (heading(h1))
      if (diceOne > diceTwo) {
        return (this.heading = "Player 1 Wins!");
      } else if (diceTwo > diceOne) {
        return (this.heading = "Player 2 Wins!");
      } else {
        this.heading = "Draw!";
      }
    },
    // Another method to reset everything and start a new game
    reset: function() {
      this.diceOne = "";
      this.diceTwo = "";
      this.diceOneImagePath = "images/bet.svg";
      this.diceTwoImagePath = "images/bet.svg";
      this.heading = "Welcome to The Game!";
      this.rolledDices = false;
      this.startGame = true;
    }
  }
};
</script>

<style>
/* importing the animate.css library CDN */
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.0.0/animate.min.css";

.game-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}

div {
  margin: 0 auto;
}
.player {
  box-shadow: inset 0px 0px 80px 0px #8c8ca4;
  width: 300px;
  height: 300px;
  border-radius: 50%;
  position: relative;
}
.player img {
  width: 70px;
  filter: invert(92%) sepia(6%) saturate(6573%) hue-rotate(288deg)
    brightness(95%) contrast(96%);
  position: absolute;
  bottom: 40%;
  left: 39%;
}
h1 {
  padding: 2rem 0;
  display: inline-block;
}
h2 {
  padding: 2rem 0;
}

/* Button Styles */
.roller {
  display: block;
  background: linear-gradient(
    45deg,
    rgba(241, 144, 190, 0.9934348739495799) 0%,
    rgba(255, 105, 149, 1) 90%
  );
  cursor: pointer;
  color: #f3fbfb;
  outline: none;
  border: none;
  padding: 1rem 2rem;
  border-radius: 50px;
  letter-spacing: 1px;
  font-size: 1rem;
  margin: 0 auto;
}
.roller > img {
  width: 30px;
}
.roller > span {
  padding: 0.5rem 0 0 0.5rem;
}

button:hover {
  opacity: 0.8;
  transition: all 0.5s ease-in-out;
}
button:hover img {
  transform: rotate(360deg);
  transition: all 0.5s ease-in;
}

/* Animation for heading */
.zoom-in-out {
  animation: zoom-in 0.5s;
}
@keyframes zoom-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
</style>