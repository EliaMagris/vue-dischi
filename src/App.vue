<template>
  <div id="app">
    <div class="logo">
      <img src="../src/assets/img/logo-small.svg" alt="" />
    </div>
    <div class="mainContainer">
      <div class="cardContainer">
        <CardsItem
          v-for="(element, index) in infoCard"
          :key="index"
          :card="element"
        />
      </div>
    </div>
  </div>
</template>

<script>
import CardsItem from "./components/CardsItem.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    CardsItem,
  },

  data() {
    return {
      infoCard: "",
    };
  },
  mounted() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((response) => {
        this.infoCard = response.data.response;
        console.log(this.infoCard);
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
  box-sizing: border-box;

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
    padding: 20px;
  }
}
</style>
