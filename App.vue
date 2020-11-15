<template>
  <div>
    <section class="game-display">
      <h1 class="title">Naughts and Crosses</h1>
      <div class="choices">
        <span
          @click="choosePlayerO"
          :style="{ color: chosenColorO }"
          class="choice choice-naught"
          >O</span
        >
        <span
          @click="choosePlayerX"
          :style="{ color: chosenColorX }"
          class="choice choice-cross"
          >X</span
        >
      </div>
      <div class="container">
        <div class="grid">
          <div
            @click="playerMove(0)"
            :style="{ color: marker0Color }"
            class="square zero"
          >
            {{ marker0 }}
          </div>
          <div
            @click="playerMove(1)"
            :style="{ color: marker1Color }"
            class="square one"
          >
            {{ marker1 }}
          </div>
          <div
            @click="playerMove(2)"
            :style="{ color: marker2Color }"
            class="square two"
          >
            {{ marker2 }}
          </div>
          <div
            @click="playerMove(3)"
            :style="{ color: marker3Color }"
            class="square three"
          >
            {{ marker3 }}
          </div>
          <div
            @click="playerMove(4)"
            :style="{ color: marker4Color }"
            class="square four"
          >
            {{ marker4 }}
          </div>
          <div
            @click="playerMove(5)"
            :style="{ color: marker5Color }"
            class="square five"
          >
            {{ marker5 }}
          </div>
          <div
            @click="playerMove(6)"
            :style="{ color: marker6Color }"
            class="square six"
          >
            {{ marker6 }}
          </div>
          <div
            @click="playerMove(7)"
            :style="{ color: marker7Color }"
            class="square seven"
          >
            {{ marker7 }}
          </div>
          <div
            @click="playerMove(8)"
            :style="{ color: marker8Color }"
            class="square eight"
          >
            {{ marker8 }}
          </div>
        </div>
      </div>
      <div class="reset-and-results">
        <h1 class="result-display">{{ result }}</h1>
        <button class="reset-button" @click="resetGame">Reset</button>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      marker0: "",
      marker1: "",
      marker2: "",
      marker3: "",
      marker4: "",
      marker5: "",
      marker6: "",
      marker7: "",
      marker8: "",

      marker0Color: "",
      marker1Color: "",
      marker2Color: "",
      marker3Color: "",
      marker4Color: "",
      marker5Color: "",
      marker6Color: "",
      marker7Color: "",
      marker8Color: "",

      winningCombos: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ],
      takenSquares: [],
      playerSquares: [],
      computerSquares: [],

      playerChoice: "",
      computerChoice: "",

      gameIsStarted: false,
      moveIsValid: null,

      chosenColorO: "",
      chosenColorX: "",

      noMsg: "",
      win: "YOU WIN",
      lose: "YOU LOSE",
      draw: `IT'S A DRAW`,
    };
  },
  computed: {
    result() {
      const checkForWinner = (arr, winningCombo) =>
        winningCombo.every((num) => arr.includes(num));

      let playerChecks = this.winningCombos.map((winningCombo) =>
        checkForWinner(this.playerSquares, winningCombo)
      );
      let computerChecks = this.winningCombos.map((winningCombo) =>
        checkForWinner(this.computerSquares, winningCombo)
      );

      if (playerChecks.includes(true)) {
        return this.win;
      } else if (computerChecks.includes(true)) {
        return this.lose;
      } else if (this.takenSquares.length >= 9) {
        return this.draw;
      } else {
        return this.noMsg;
      }
    },
  },
  methods: {
    choosePlayerO() {
      this.gameIsStarted = true;
      this.playerChoice = "O";
      this.computerChoice = "X";

      this.chosenColorO = "#5794d9";
      this.chosenColorX = "#db5a6e";
    },
    choosePlayerX() {
      this.gameIsStarted = true;
      this.playerChoice = "X";
      this.computerChoice = "O";

      this.chosenColorX = "#5794d9";
      this.chosenColorO = "#db5a6e";
    },
    checkIfMoveIsValid(num) {
      return !this.takenSquares.includes(num) && this.gameIsStarted === true
        ? true
        : false;
    },
    playerMove(num) {
      let moveIsValid = this.checkIfMoveIsValid(num);

      if (moveIsValid) {
        switch (num) {
          case 0:
            this.marker0 = this.playerChoice;
            this.marker0Color = "#5794d9";
            break;
          case 1:
            this.marker1 = this.playerChoice;
            this.marker1Color = "#5794d9";
            break;
          case 2:
            this.marker2 = this.playerChoice;
            this.marker2Color = "#5794d9";
            break;
          case 3:
            this.marker3 = this.playerChoice;
            this.marker3Color = "#5794d9";
            break;
          case 4:
            this.marker4 = this.playerChoice;
            this.marker4Color = "#5794d9";
            break;
          case 5:
            this.marker5 = this.playerChoice;
            this.marker5Color = "#5794d9";
            break;
          case 6:
            this.marker6 = this.playerChoice;
            this.marker6Color = "#5794d9";
            break;
          case 7:
            this.marker7 = this.playerChoice;
            this.marker7Color = "#5794d9";
            break;
          case 8:
            this.marker8 = this.playerChoice;
            this.marker8Color = "#5794d9";
            break;
        }
        this.playerSquares.push(num);
        this.takenSquares.push(num);
        this.computerMove();
        this.checkIfGameIsOver();
      }
    },
    computerMove() {
      let nums = [0, 1, 2, 3, 4, 5, 6, 7, 8];
      let filteredNums = nums.filter((x) => !this.takenSquares.includes(x));
      let randomIndex = Math.floor(Math.random() * filteredNums.length);
      let num = filteredNums[randomIndex];
      switch (num) {
        case 0:
          this.marker0 = this.computerChoice;
          this.marker0Color = "#db5a6e";
          break;
        case 1:
          this.marker1 = this.computerChoice;
          this.marker1Color = "#db5a6e";
          break;
        case 2:
          this.marker2 = this.computerChoice;
          this.marker2Color = "#db5a6e";
          break;
        case 3:
          this.marker3 = this.computerChoice;
          this.marker3Color = "#db5a6e";
          break;
        case 4:
          this.marker4 = this.computerChoice;
          this.marker4Color = "#db5a6e";
          break;
        case 5:
          this.marker5 = this.computerChoice;
          this.marker5Color = "#db5a6e";
          break;
        case 6:
          this.marker6 = this.computerChoice;
          this.marker6Color = "#db5a6e";
          break;
        case 7:
          this.marker7 = this.computerChoice;
          this.marker7Color = "#db5a6e";
          break;
        case 8:
          this.marker8 = this.computerChoice;
          this.marker8Color = "#db5a6e";
          break;
      }
      this.computerSquares.push(num);
      this.takenSquares.push(num);
      this.checkIfGameIsOver();
    },
    checkIfGameIsOver() {
      if (
        this.result === this.win ||
        this.result === this.lose ||
        this.result === this.draw
      ) {
        this.gameIsStarted = false;
        this.playerChoice = "";
        this.computerChoice = "";
      }
    },
    resetGame() {
      this.marker0 = "";
      this.marker1 = "";
      this.marker2 = "";
      this.marker3 = "";
      this.marker4 = "";
      this.marker5 = "";
      this.marker6 = "";
      this.marker7 = "";
      this.marker8 = "";

      this.takenSquares = [];
      this.playerSquares = [];
      this.computerSquares = [];

      this.playerChoice = "";
      this.computerChoice = "";
      this.chosenColorO = "";
      this.chosenColorX = "";

      this.gameIsStarted = false;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:wght@100&display=swap");

* {
  box-sizing: border-box;
  font-family: "Raleway", sans-serif;
}

body {
  margin: 0;
  padding: 0;
  background: #E7DBB7;
}

.game-display {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.title {
  margin: 0;
  padding: 0;
  font-size: 2em;
  text-align: center;
}

.choices {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin-top: 0.5em;
}

.choice {
  font-size: 2em;
  margin: 0 0.5em;
  padding: 0.5em;
  font-weight: bold;
}

.choice-naught:hover {
  color: #5794d9;
  cursor: pointer;
}
.choice-cross:hover {
  color: #5794d9;
  cursor: pointer;
}

.container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50vh;
  margin: 0;
  background: white;
}

.grid {
  display: grid;
  position: absolute;
  margin: 0;
  padding: 0;
  grid-template-columns: 12vh 12vh 12vh;
  grid-template-rows: auto auto auto;
  height: 36vh;
  width: 36vh;
}

.square {
  position: relative;
  height: 12vh;
  width: 12vh;
  border: 1px solid black;
  font-size: 2rem;
  font-weight: bold;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.square:hover {
  background: rgba(0, 0, 0, 0.1);
}

/* square borders */
.zero,
.one,
.two {
  border-top: none;
}
.six,
.seven,
.eight {
  border-bottom: none;
}
.zero,
.three,
.six {
  border-left: none;
}
.two,
.five,
.eight {
  border-right: none;
}

.reset-and-results {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.reset-button {
  background: transparent;
  border: 1px solid black;
}

.reset-button:hover {
  background: rgba(0, 0, 0, 0.1);
  cursor: pointer;
}

.result-display {
  margin-top: 10px;
}
</style>