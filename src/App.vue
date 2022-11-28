<template>
  <div id="app">
    <div class="logo">
      <img src="../src/assets/img/logo-small.svg" alt="" />
    </div>
    <div>
      <select name="" id="" v-model="selectGen">
        <option :value="elem" v-for="(elem, index) in infoSelect" :key="index">{{ elem }}</option>
      </select>
    </div>
    <div class="mainContainer">
      <div class="cardContainer">
        <CardsItem
          v-for="(element, index) in infoCard"
          :key="index"
          :card="element"
          :class="element.genre == selectGen ? 'd-block' : 'd-none'"
        />
      </div>
    </div>
  </div>
</template>

<script>
import CardsItem from './components/CardsItem.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    CardsItem,
  },

  data() {
    return {
      infoCard: [],
      infoSelect: [],
      selectGen: '',
    };
  },

  mounted() {
    axios.get('https://flynn.boolean.careers/exercises/api/array/music').then((response) => {
      this.infoCard = response.data.response;
      console.log(this.infoCard);
      this.infoCard.forEach((SingleGen) => {
        if (!this.infoSelect.includes(SingleGen.genre)) {
          this.infoSelect.push(SingleGen.genre);
        }
      });
    });
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: rgb(30, 45, 59);

  .logo {
    padding: 15px;
    text-align: start;
    background-color: rgb(46, 58, 70);
    img {
      width: 3%;
    }
  }

  .mainContainer {
    display: flex;
    justify-content: center;
  }

  .cardContainer {
    display: flex;
    flex-wrap: wrap;
    width: 80%;
    padding: 80px 100px;
  }
}
</style>
