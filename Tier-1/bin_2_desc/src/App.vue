<template>
  <div id="app" class="container mx-auto pt-16">
    <h1>Bin2Dec</h1>
    <div class="flex flex-row content-center -mx-2 mt-20">
      <div class="px-2 ml-auto">
        <label class="label-form" for="binary">Binary</label>
        <input
          id="binary"
          type="text"
          class="input-form focus:outline-none focus:bg-white focus:border-gray-500"
          v-model="binary"
        />
        <p
          v-if="invalidBinary"
          class="text-red-500 text-xs italic"
        >Binary invalid! Only 1 and 0 are accepted.</p>
      </div>
      <div class="px-2">
        <label class="label-form" for="decimal">Decimal</label>
        <input
          id="decimal"
          type="text"
          class="input-form focus:outline-none focus:bg-white focus:border-gray-500"
          v-model="decimal"
        />
      </div>

      <div class="px-2 mr-auto pt-3">
        <button class="btn btn-blue mt-4" @click="convert()">Convert</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      binary: 0,
      decimal: 0,
      invalidBinary: false
    };
  },

  watch: {
    binary(value) {
      // Verifying if the number inputted is only 0 and 1
      return (this.invalidBinary = !/^[0-1]+$/.test(value));
    }
  },

  methods: {
    convert() {
      if (this.invalidBinary) {
        return;
      }

      // Reverse Binary to iterate from back
      const reversedBynary = this.binary
        .split("")
        .map(Number)
        .reverse();

      // Calculate the result applying (value * (base ^ index)) and 
      // accumulating with the previous result;
      this.decimal = reversedBynary.reduce(
        (accumulator, currentValue, index) =>
          accumulator + currentValue * Math.pow(2, index)
      );
    }
  }
};
</script>