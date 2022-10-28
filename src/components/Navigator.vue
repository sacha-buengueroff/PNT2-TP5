<template>

  <section class="src-components-navigator">
    <div id="navigator">
      <button id="reset" @click="botonRestart()">{{ restartMessage }}</button>
      <span id="message"> {{ message }} </span>

      <button id="easy" :class="!isHard" @click="easyButton()">easy</button>
      <button id="hard" :class="isHard" @click="hardButton()">hard</button>
    </div>
    <Container :squares="squares" :picked-color="pickedColor" @color-correcto="setAllColorsTo(pickedColor)" @color-incorrecto="incorrectColor($event)"/>
  </section>
  
</template>

<script>
  import Container from './Container.vue'

  export default  {
    name: 'src-components-navigator',
    props: [],
    mounted() {
      this.createSquares(this.colorCount)
    },
    components: {
      Container
    },
    data () {
      return {
        isHard: true,
        squares: [],
        colorCount: 6,
        hardColor: 6,
        easyColor: 3,
        pickedColor: "",
        message: "",
        restartMessage: "New Colors!"
      }
    },
    methods: {
      easyButton() {
        if (this.isHard) {
          this.isHard = false
          this.colorCount = this.easyColor;
          this.botonRestart()
        }
      },
      hardButton() {
        if (!this.isHard) {
          this.isHard = true
          this.colorCount = this.hardColor;
          this.botonRestart()
        }
      },
      createSquares(quantity) {
        var arr = [];
        for (var i = 0; i < quantity; i++) {
          arr.push(this.createRandomStringColor());
        }
        this.squares = arr
        this.pickedColor = arr[Math.floor(Math.random() * this.colorCount)]
        this.$emit("picked-color", this.pickedColor)
      },
      createRandomStringColor(){
        var newColor = "rgb(" + this.randomInt() + ", " + this.randomInt() + ", " + this.randomInt() + ")" ;
        return newColor;
      },
      randomInt(){
        return Math.floor(Math.random() * 256);
      },
      botonRestart() {
        this.createSquares(this.colorCount)
        this.message = ""
        this.$emit('color-correcto', "steelblue")
      },
      setAllColorsTo(color) {
        let arr = []
        for (let i = 0; i < this.squares.length; i++) {
          arr[i] = color
        }
        this.squares = arr
        this.message = "You Picked Right!"
        this.restartMessage = "Play Again!"
        this.$emit('color-correcto', color)
      },
      incorrectColor(index) {
        let arr = [...this.squares]
        arr[index] = "#232323"
        this.squares = arr
        this.message = "Try Again!"
      }
    },
    computed: {
      
    }
}

</script>

<style scoped lang="css">
  #navigator {
    background: #ffffff;
    height: 30px;
    text-align: center;
    margin: 0;
    margin-top: -30px;
  }
  #message {
    color: #000000;
    display: inline-block;
    width: 20%;
  }
  button {
    border: none;
    background-color: white;
    font-family: "Montserrat", "Avenir";
    text-transform: uppercase;
    height: 100%;
    font-weight: 700;
    letter-spacing: 1px;
    color: steelblue;
    transition: all 0.3s;
    outline: none;
  }
  button:hover {
    color: white;
    background-color: steelblue;
  }
  .selected {
    background-color: steelblue;
    color: white;
  }
</style>
