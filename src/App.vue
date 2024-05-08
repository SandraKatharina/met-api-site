<template>
  <section class="main-section">
    <div class="object-box">
      <h1>Title: {{ artObject.title }}, dated :{{ artObject.objectDate }}</h1>
      <div class="img-container" v-if="artObject.primaryImageSmall == 0">Sorry no image</div>
      <img v-else-if="artObject.primaryImageSmall" :src="artObject.primaryImageSmall" />
    </div>
    <button @click="showRandomArtObject">SHOW ME A RANDOM OBJECT!</button>
  </section>
</template>

<script>
function randomizeInRange(min, max) {
  return Math.floor(Math.random() * (max - min) + min)
}

export default {
  data() {
    return {
      artObject: {},
      resultList: {}
    }
  },
  methods: {
    showRandomArtObject(value) {
      console.log(value)
      window.location.reload()
    }
  },
  async created() {
    const randomNumber = randomizeInRange(1, 470000)
    const response = await fetch(
      'https://collectionapi.metmuseum.org/public/collection/v1/objects/' + randomNumber
    )
    const result = await response.json()

    this.artObject = result
    console.log(result)
  }
}
</script>

<style scoped>
.main-section {
  display: flex;
  gap: 80px;
  margin: auto;
  width: 900px;
}

.main-section > div {
  background-color: coral;
  width: 600px;
  min-height: 600px;

  border: 2px solid #422800;
  border-radius: 30px;
  box-shadow: #422800 4px 4px 0 0;
  color: #422800;

  font-weight: 600;
  font-size: 18px;
  padding: 0 16px;
  line-height: 50px;
  text-align: center;
  text-decoration: none;
  padding: 0 25px;
}

.object-box {
  display: flex;
  flex-direction: column;
  align-content: space-around;
}

.img-container {
  overflow: hidden;
}

img {
  max-width: 100%;
}

button {
  background-color: lightcoral;
  border: 2px solid #422800;
  border-radius: 100%;
  box-shadow: #422800 4px 4px 0 0;
  color: #422800;
  cursor: pointer;
  display: inline-block;
  font-weight: 600;
  font-size: 18px;
  padding: 0 16px;
  line-height: 50px;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 200px;
  height: 200px;
  padding: 0 25px;
}

button:hover {
  background-color: steelblue;
}

button:active {
  box-shadow: #422800 2px 2px 0 0;
  transform: translate(2px, 2px);
}
</style>
