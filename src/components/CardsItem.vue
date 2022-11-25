<template>
  <div class="container">
    <div class="card" style="width: 18rem">
      <img :src="card.poster" class="card-img-top" alt="..." />
      <div class="card-body">
        <h5 class="card-title">{{ card.title }}</h5>

        <div class="card-text">
          <div>{{ card.author }}</div>
          <div>{{ card.year }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardsItem',
  props: {
    card: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  width: calc(100% / 5);
  margin-top: 30px;

  .card {
    width: 100% !important;
    height: 100%;
    margin: 5px;
    background-color: rgb(46, 58, 70);

    img {
      padding: 10px;
    }

    .card-title {
      color: white;
      font-weight: bold;
    }

    .card-text {
      color: gray;
    }
  }
}
</style>
