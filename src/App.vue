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
    roll(sides) {
      return Math.floor(Math.random() * sides) + 1
    },
    rollD20() {
      this.result = this.roll(20)
    },
    parseDice(notation) {
      const rgx = /^(\d*)d(\d+)([+-]\d+)?$/
      const match = notation.match(rgx)

      if (!match) throw new Error("Invalid dice notation")

      return {
        amount: match[1] ? parseInt(match[1], 10) : 1,
        sides: parseInt(match[2], 10),
        mod: match[3] ? parseInt(match[3], 10) : 0
      }
    }
  },
  mounted() {
    const params = new URLSearchParams(window.location.search)

    if (params.has('q')) {
      const { amount, sides, mod } = this.parseDice(params.get('q'))

      let total = 0
      for (let i = 0; i < amount; i++) {
        const rolled = this.roll(sides)

        console.info(`[${i}] rolled ${rolled}`)
        total += rolled
      }

      this.result = total + mod
    }
    else {
      this.rollD20()
    }
  }
}
</script>