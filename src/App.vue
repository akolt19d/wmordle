<template>
    <NavComponent @toggle="toggleHelp"/>
    <main>
      <input
        :value="input"
        class="input"
        @input="onInputChange"
        placeholder="Tap on the virtual keyboard to start"
      >
      <GameComponent/>
      <SimpleKeyboard @onChange="onChange" @onKeyPress="onKeyPress" :input="input" @enter="verifyWord"/>
      <PopupBig v-if="isGameWon == true" type="victoryScreen" @copy="shareResult"/>
      <PopupBig type="helpPopup" @toggle="toggleHelp" v-if=" showHelp == true"/>
    </main>
</template>

<script>
import SimpleKeyboard from "./components/Keyboard";
import "./styles/Keyboard.scss";
import NavComponent from "./components/Nav"
import GameComponent from "./components/Game";
import PopupBig from "./components/PopupBig";

export default {
  name: "App",
  components: {
    SimpleKeyboard,
    NavComponent,
    GameComponent,
    PopupBig
  },
  data: () => ({
    input: "",
    row: 1,
    word: "lewek",
    isGameWon: false,
    showHelp: false
  }),
  methods: {
    verifyWord() {
      if(this.input.length == 5)
      {
        for(let i = 0; i < 5; i++)
        {
          let grid = document.querySelector(`#grid${this.row}${i + 1}`)
          grid.style.transform = "rotateY(360deg)"

          for(let j = 0; j < 5; j++)
          {
            if(grid.innerHTML == this.word[j].toUpperCase())
            {
              grid.className = "grid yellow"
            }
          }
          if(this.input[i] == this.word[i].toUpperCase())
            grid.className = "grid green"
        }
        if(this.input == this.word.toUpperCase())
        {
          setTimeout(() => {
            this.isGameWon = true;
          }, 1000);
        }
        this.input = ""
        if(this.row < 6)
            this.row++
      }
      else
      {
        for(let i = 0; i < 5; i++)
        {
          let grid = document.querySelector(`#grid${this.row}${i + 1}`)
          grid.style.animation = "shake .25s"
          setTimeout(() => {
            grid.style.animation = "none"
          }, 250);
        }
      }
    },
    onChange(input) {
      this.input = input;
      if(this.input.length <= 5)
      {
  
        for(let i = 0; i < input.length; i++)
        {
            document.querySelector(`#grid${this.row}${i + 1}`).innerHTML = input[i]
        }
  
        // if(this.input.length == 5)
        // {
        //   console.log("essa")
        //   this.verifyWord()
        //   this.input = ""
        //   if(this.row < 6)
        //   this.row++
        // }
      }
      else
      {
        this.input = this.input.substring(0, 5)
      }
    },
    onKeyPress(button) {
      //console.log("button", button);

      if(button == "{bksp}" && this.input.length > 0)
      {
          document.querySelector(`#grid${this.row}${this.input.length}`).innerHTML = ""
      }
    },
    onInputChange(input) {
      this.input = input.target.value;
    },
    toggleHelp() {
      if(this.showHelp == false)
      {
        this.showHelp = true 
      }
      else
      {
        this.showHelp = false
      } 

      //console.log("omamale")
    }
    // shareResult() {
    //   console.log("Wmordle<br>essa")
      
    //   let clipboard = new ClipboardItem
    // }
  }
};
</script>

<style lang="scss">
* 
{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body 
{
    background-color: $bg;
    font-family: $font-main;
    color: $secondary;
    font-weight: lighter;
    overflow: hidden;
}
nav
{
    width: 100vw;
    height: 50px;
    @include fc;
    justify-content: space-around;
    border-bottom: .3px solid $accent;
    h1 
    {
        color: $accent;
        font-family: $font-acc;
    }
}
main 
{
    height: 94vh;
    width: 100vw;
    @include fc;
    input
    {
        display: none;
    }
    #grid
    {
        height: clamp(100px, 45vh, 500px);
        aspect-ratio: 5/6;
        max-width: 90vw;
        display: grid;
        grid-template-rows: repeat(6, 1fr);
        grid-template-columns: repeat(5, 1fr);
        gap: 15px;
        position: relative;
        bottom: 130px;
        .grid 
        {
            border: 0.3px solid rgba($secondary, .5);
            @include fc;
            font-size: 150%;
            font-weight: bold;
            transition: .8s color, .8s background-color, .8s transform;
        }
        .yellow
        {
          background-color: $yellow;
          color: #1b1b1b;
          //transform: rotateX(360deg);
        }
        .green
        {
          background-color: $accent;
          color: #1b1b1b;
        }
        .reveal
        {
          transform: rotateX(360deg);
        }
    }
    // #grid 
    // {
    //     height: clamp(100px, 45vh, 500px);
    //     aspect-ratio: 5/6;
    //     display: grid;
    //     grid-template-rows: repeat(6, 1fr);
    //     grid-template-columns: repeat(5, 1fr);
    //     gap: 15px;
    //     .grid 
    //     {
    //         border: 0.3px solid $secondary;
    //         @include fc;
    //     }
    // }
    // #keyboard 
    // {
    //     position: absolute;
    //     bottom: 0;
    // }
}
// #app {
//   font-family: $font-main;
//   -webkit-font-smoothing: antialiased;
//   -moz-osx-font-smoothing: grayscale;
//   background: $bg;
//   height: 100vw;
//   width: 100vh;
// }
</style>
