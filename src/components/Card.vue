<template>
  <div class="card">
    <img :src="require(`@/assets/cards/${card}.png`)" alt="" />
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["card"],
  data() {
    return {
      
    };
  },
};
</script>

<style scoped lang="scss">
.card {
  width: 100px;
  height: 150px;
  object-fit: contain;
  margin: 0 10px;
  border: 1px solid #808080;
  img{
    width: 100%;
    height: 100%;
  }
}
</style>
