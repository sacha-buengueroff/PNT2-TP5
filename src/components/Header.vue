<template>

  <section class="src-components-header">

    <div id="header" :style="{'background': colorCorrecto}">
      <h1>The Great <br>
        <span id="colorDisplay">{{ pickedColor }}</span>
        <br>
        Guessing Game</h1>
    </div>

    <Navigator @picked-color="pickedColor=$event" @color-correcto="modifyColor($event)"/>
  </section>

</template>

<script>
  import Navigator from './Navigator.vue'

  export default  {
    name: 'src-components-header',
    props: [],
    components: {
      Navigator
    },
    mounted () {
    
    },
    data () {
      return {
        pickedColor: "",
        colorCorrecto: "steelblue"
      }
    },
    methods: {
      modifyColor(color) {
        this.colorCorrecto = color
      }
    },
    computed: {

    }
}

</script>

<style scoped lang="css">
  #header {
    transition: all 0.3s;
    background: steelblue;
    text-transform: uppercase;
    text-align: center;
    margin: 0;
    color: white;
    
  }
  #colorDisplay {
    font-size: 200%;
  }
</style>
