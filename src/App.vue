<template>
  <div id="app">
    <headerBig/>
    <div>
      <select name="" id="" v-model="selectGen">
        <option value="" selected>SEE ALL</option>
        <option :value="elem" v-for="(elem, index) in infoSelect" :key="index">{{ elem }}</option>
      </select>
    </div>
    <div class="mainContainer">
      <div class="cardContainer">
        <CardsItem
          v-for="(element, index) in funzioneControllo"
          :key="index"
          :card="element"
        />
      </div>
    </div>
  </div>
</template>

<script>
import CardsItem from './components/CardsItem.vue';
import headerBig from './components/headerBig.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    CardsItem,
    headerBig
  },

  data() {
    return {
      infoCard: [],
      infoSelect: [],
      selectGen: [],
    };
  },

  computed: {
    funzioneControllo(){
      if (this.selectGen == ""){
        return this.infoCard
      }else{
        return this.infoCard.filter((elem) =>{
          return elem.genre == this.selectGen
        })
      }
    }

  },

  mounted() {
    this.filterImage()
  },

  methods: {
    filterImage(){
      axios.get('https://flynn.boolean.careers/exercises/api/array/music').then((response) => {
      this.infoCard = response.data.response;
      console.log(this.infoCard);
      this.infoCard.forEach((SingleGen) => {
        if (!this.infoSelect.includes(SingleGen.genre)) {
          this.infoSelect.push(SingleGen.genre);
        }
      });
    });
    }
  }
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
