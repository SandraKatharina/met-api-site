<template>
  <div>
    <h1>Title: {{ artObject.title }}, dated :{{ artObject.objectDate }}</h1>
    <div v-if="artObject.primaryImageSmall.length == 0">Sorry no image</div>
    <img v-else :src="artObject.primaryImageSmall" />
  </div>
  <button @click="showRandomArtObject">SHOW ME SOMETHING RANDOM!</button>
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
  async created() {
    const randomNumber = 2845
    const response = await fetch(
      'https://collectionapi.metmuseum.org/public/collection/v1/objects/' + randomNumber
    )
    const result = await response.json()

    this.artObject = result
    console.log(result)
  }
}
</script>

<style scoped></style>
