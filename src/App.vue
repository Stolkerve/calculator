<template>
  <div id='app'>
    <div class='calculator-conteiner'>
      <div class='screen'>
        {{buffer}}
      </div>
      <div class='pad-conteiner'>
        <div class='pad-numbers'>
          <template v-for="(row) in pad">
            <template v-for="(col) in row">
                <Button :text="col" :callBack="handleBuffer" :key="col"/>
            </template>
          </template>
        </div>
        <!--
        <div class='pad-numbers'>
          <template v-for="(row) in pad">
            <template v-for="(col) in row">
                <Button :text="col" :callBack="handleBuffer" :key="col"/>
            </template>
          </template>
        </div>
        -->
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Button from './components/Button.vue'
import Screen from './components/Screen.vue'
@Component({
  components: {
    Button
  }
})
export default class App extends Vue {
  private pad:string[][] = [
    ['1', '2', '3', 'CE'],
    ['4', '5', '6', '+'],
    ['7', '8', '9', '-'],
    ['(', '0', ')', '*'],
    ['=', '.', '/']
  ];
  private buffer:string = '1+2';

  handleBuffer(text:string) {
    if(text === 'CE' && this.buffer !== 'ERROR')
    {
      this.buffer = this.buffer.slice(0, -1);
    }
    else if (text === '=')
    {
      this.calculateBuffer();
    }
    else if (this.buffer === 'ERROR')
    {
      this.buffer = '';
    }
    else
    {
      this.buffer += text;
    }
  }

  calculateBuffer() {
    try {
      const sum = new Function('return ' + this.buffer);
      this.buffer = String(sum());
    }
    catch (e) {
      this.buffer = 'ERROR'
      console.log(e.message, ' Er')
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
  justify-content: center;
  display: flex;
}

.calculator-conteiner {
  border: 3px solid rgb(5, 5, 5);
  max-width: min-content;
}

.screen {
  background-color: rgb(147, 184, 130) ;
  height: 70px;
  border-bottom: 3px solid black;
  font-family: 'DotGothic16';
  font-size: 34px;
  text-align: right;
  overflow-x: scroll;
}

.pad-conteiner{
  background-color: black;
  display: flex;
}

.pad-numbers {
  display: grid;
  grid-template-columns: repeat(4, 70px);
  grid-template-rows:    repeat(5, 55px);
  gap: 3px;
}

</style>
