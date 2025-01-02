<template>
  <article>
    <span>{{ result }}</span>

    <button v-on:click="rollD20()" type="button">Reroll</button>
  </article>
</template>

<style scoped>
span {
  font-size: 9rem;
  display: grid;
  place-content: center center;
}

button {
  width: 100%;
}
</style>

<script>
export default {
  data() {
    return {
      result: null
    }
  },
  methods: {
    rollD20() {
      this.result = Math.floor(Math.random() * 20) + 1
    }
  },
  mounted() {
    this.rollD20()
  }
}
</script>