<template>
  <div id="app">
    <h1>Desafío - Templates y rendering en Vue</h1>
    <div class="container">
      <div class="form-container">
        <h2>Estilo Dinámico</h2>
        <form>
          <div>
            <label for="width">Ancho:</label>
            <input type="number" id="width" v-model="width">
          </div>
          <div>
            <label for="height">Alto:</label>
            <input type="number" id="height" v-model="height">
          </div>
          <div>
            <label for="radius">Radio:</label>
            <input type="number" id="radius" v-model="radius">
          </div>
          <div>
            <label for="rotation">Rotación:</label>
            <input type="number" id="rotation" v-model="rotation">
          </div>
          <div>
            <label for="color">Color de fondo:</label>
            <input type="color" id="color" v-model="color">
          </div>
          <div>
            <label for="textColor">Color de texto:</label>
            <input type="color" id="textColor" v-model="textColor">
          </div>
          <div>
            <label for="text">Texto a mostrar:</label>
            <input type="text" id="text" v-model="text">
          </div>
          <div>
            <label for="font">Tipografía:</label>
            <select id="font" v-model="font">
              <option value="Arial">Arial</option>
              <option value="Verdana">Verdana</option>
              <option value="Times New Roman">Times New Roman</option>
              <option value="Courier">Courier</option>
            </select>
          </div>
          <div>
            <label>Tamaño de letra:</label>
            <label>
              <input type="radio" v-model="fontSize" value="small"> Pequeña
            </label>
            <label>
              <input type="radio" v-model="fontSize" value="medium"> Mediana
            </label>
            <label>
              <input type="radio" v-model="fontSize" value="large"> Grande
            </label>
          </div>
          <div>
            <label>
              <input type="checkbox" v-model="showFigure"> Mostrar figura
            </label>
          </div>
          <div>
            <label>
              <input type="checkbox" v-model="showText"> Mostrar texto
            </label>
          </div>
        </form>
      </div>
      <Figure 
        :width="width"
        :height="height"
        :radius="radius"
        :rotation="rotation"
        :color="color"
        :text-color="textColor"
        :text="text"
        :font="font"
        :font-size="fontSize"
        :show-figure="showFigure"
        :show-text="showText"
        @color-used="addUsedColor"
      />
    </div>
    <div class="color-list">
      <h3>Colores utilizados:</h3>
      <ul>
        <li v-for="(usedColor, index) in usedColors" :key="index" :style="{ color: usedColor }">
          {{ usedColor }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Figure from './components/Figure.vue'

export default {
  name: 'App',
  components: {
    Figure
  },
  data() {
    return {
      width: 100,
      height: 100,
      radius: 0,
      rotation: 0,
      color: '#000000',
      textColor: '#FFFFFF',
      text: 'Hola Mundo',
      font: 'Arial',
      fontSize: 'medium',
      showFigure: true,
      showText: true,
      usedColors: []
    }
  },
  methods: {
    addUsedColor(color) {
      if (!this.usedColors.includes(color)) {
        this.usedColors.push(color)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.container {
  display: flex;
  justify-content: space-between;
}

.form-container {
  width: 45%;
}

form div {
  margin-bottom: 10px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input, select {
  width: 100%;
}

.color-list {
  margin-top: 20px;
}

ul {
  list-style-type: none;
  padding: 0;
}
</style>
