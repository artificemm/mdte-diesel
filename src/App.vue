<template>
  <div id="app">
    <div id="display" class="calculator-screen">
      <p>
        <i class="fas fa-tachometer-alt"></i>
        {{ selected_tank }}
      </p>
      <p>
        <i class="fas fa-ruler-vertical"></i>
        {{ selected_index }} cm
      </p>
      <div class="columns">
        <div class="column">
          <h1 class="result">
            <i class="fas fa-flask"></i>
            {{ lookup }} l
          </h1>
        </div>
      </div>
    </div>
    <div class="calculator-keys">
      <button v-for="tank in Object.keys(this.table)" :value="tank" @click="setTank(tank)" class="button">{{tank}}</button>
    </div>
    <div class="calculator-keys function-keys">
      <button @click="reset_lookup" class="button">C</button>
      <button @click="decreaseIndex" class="button">-</button>
      <button @click="increaseIndex" class="button">+</button>      
    </div>

    <div id="slider">
      <h2>Altura: </h2>
      <br/>
      <div class="index_slider">
        <vue-slider ref="slider" v-model="selected_index" :min="0" :max="31" size="360px"></vue-slider>
      </div>
    </div>
  </div>
</template>

<script>
import vueSlider from 'vue-slider-component'
export default {
  name: 'app',
  components: {
    vueSlider
  },
  data() {
    return {
      selected_tank: '284',
      selected_index: 0,
      table: {
        '284': [0.00, 1.98, 5.56, 10.16, 15.50, 21.65,28.28,35.46, 43.08, 51.13, 59.73, 68.33, 77.59, 86.85, 96.50, 106.46, 116.61, 126.97, 137.55, 148.32, 159.27, 170.34, 181.63, 193.00, 204.51, 218.18, 227.87, 239.72, 251.68, 263.73, 275.85, 288.05],
        '379': [0.00,1.80, 5.05, 9.21, 14.13, 19.66, 25.68, 32.70, 39.13, 46.43, 54.10, 62.21, 70.33, 78.88, 87.64, 96.68, 105.88, 115.27, 124.88, 134.64, 144.56, 154.58, 164.80, 175.07, 185.46, 195.99, 206.52, 217.18, 227.91, 238.71, 249.55, 260.43],
        '454': [0.00, 1.61, 4.53, 8.29, 12.69, 17.67, 23.08, 28.94, 35.17, 41.73, 48.63, 55.79, 63.22, 70.90, 78.89, 86.89, 95.15, 103.61, 112.21, 120.96, 129.84, 138.82, 147.96, 157.13, 166.41, 175.79, 185.17, 194.64, 204.13, 213.68, 223.24, 232.80],
        '511': [0.00, 1.33, 3.74, 6.85, 10.48, 14.59, 19.05, 23.90, 29.04, 34.46, 40.16, 46.06, 52.21, 58.63, 65.05, 71.75, 78.57, 85.54, 92.66, 99.88, 107.22, 114.63, 122.18, 129.75, 137.41, 145.16, 152.90, 160.72, 168.56, 176.44, 184.34, 192.23],
        '568': [0.00, 1.03, 2.88, 5.27, 8.07, 11.24, 14.67, 18.40, 22.36, 26.54, 30.92, 35.47, 40.20, 45.08, 50.09, 55.40, 60.71, 65.88, 71.35, 76.82, 82.56, 88.27, 94.09, 99.92, 105.82, 111.78, 117.75, 123.77, 129.81, 135.88, 141.96, 148.04]
      }
    }
  },
  computed: {
  lookup: function () {
    return this.table[this.selected_tank][this.selected_index]
    }
  },
  methods: {
    reset_lookup: function () {
      this.selected_tank = '284'
      this.selected_index = 0
    },
    setTank: function (tank) {
      this.selected_tank = tank
    },
    increaseIndex: function () {
      if (this.selected_index < 31) {
        this.selected_index += 1
      }
    },
    decreaseIndex: function () {
      if (this.selected_index > 0) {
        this.selected_index -= 1
      }
    }
  }
}
</script>

<style>

html {
  font-size: 62.5%;
  box-sizing: border-box;
}

*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

.calculator-screen {
  width: 100%;
  /*font-size: 5rem;*/
  height: 80px;
  border: none;
  background-color: #252525;
  color: #fff;
  text-align: right;
  padding-right: 20px;
  padding-left: 10px;
}

.calculator-keys {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
  padding: 20px;
}

.index_slider {
  width: 80%;
  margin: 0 auto;
}
</style>
