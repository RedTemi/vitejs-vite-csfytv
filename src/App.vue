<template>
  <!-- RECOMMENDATION: Look at src/components/Penguin.vue, first to see visual feedback -->
  <div id="app">
    <div>
      <h2>List of Penguins</h2>
      <!-- These two buttons are linked to the methods found below -->
      <button @click="moveBestPenguinToTop">Move best penguin to top</button>
      <button @click="moveWorstPenguinToBottom">
        Move worst penguin to bottom
      </button>
      <!-- Visit Penguin.vue and make this data display -->
      <penguin
        v-for="penguin in penguins"
        :key="penguin.name"
        :penguin="penguin"
      />
    </div>

    <div>
      <h2>Best Penguin</h2>
      <penguin :penguin="bestPenguin" />
    </div>

    <div>
      <h2>Worst Penguin</h2>
      <penguin :penguin="worstPenguin" />
    </div>
  </div>
</template>

<script>
import Penguin from './components/Penguin.vue';
export default {
  name: 'App',
  components: {
    Penguin,
  },
  computed: {
    // NOTE: these computed values will be utilized by the Penguin.vue component ( see template )
    bestPenguin() {
      var highest = { rating: Number.MIN_VALUE };
      this.penguins.forEach((penguin) => {
        if (penguin.rating > highest.rating) {
          highest = penguin;
        }
      });
      // find the penguin with the highest rating in the array and return it
      // access the penguin list using `this.penguins`
      return highest;
    },

    worstPenguin() {
      var lowest = { rating: Number.MAX_VALUE };
      this.penguins.forEach((penguin) => {
        if (penguin.rating < lowest.rating) {
          lowest = penguin;
        }
      });
      // find the penguin with the lowest rating in the array and return it
      return lowest;
    },
  },

  methods: {
    moveBestPenguinToTop() {
      let pos1 = this.penguins[0];
      let pos1_copy = { ...pos1 };
      let posMax = this.penguins.indexOf(this.bestPenguin);
      if (posMax === 0) {
        return;
      } else {
        this.penguins[0] = this.bestPenguin;
        this.penguins[posMax] = pos1_copy;
      }
      // move the highest-rated penguin to the top of the list
      // Do not sort the entire array, ONLY move the best penguin
      console.log(this.penguins)
    },

    moveWorstPenguinToBottom() {
      let posLeast = this.penguins.indexOf(this.worstPenguin);
      let least_copy = {...this.worstPenguin}
      if (posLeast === this.penguins.lenght-1) {
        return;
      } else {
        this.penguins.splice(posLeast, 1);
        this.penguins.push(least_copy)
      }
      // move the worst-rated penguin to the bottom of the list
      // Do not sort the entire array, ONLY move the worst penguin
    },
  },
  data() {
    return {
      penguins: [
        {
          name: 'Yellow Eyed',
          rating: 4,
        },
        {
          name: 'Humboldt',
          rating: 4,
        },
        {
          name: 'Emperor',
          rating: 1,
        },
        {
          name: 'King',
          rating: 5,
        },
        {
          name: 'Fiordland',
          rating: 2,
        },
        {
          name: 'Snares',
          rating: 3,
        },
      ],
    };
  },
};
</script>

<style></style>
