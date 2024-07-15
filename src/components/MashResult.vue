<template>
  <div class="mash-result my-8" v-if="result">
    <h2 class="text-xl mb-4 text-center">Your Future</h2>
    <ul class="w-1/2 m-auto">
      <li v-for="(res, index) in result" :key="index" class="p-1 m-1 flex border-b">
        <div class="w-1/2 font-bold text-primary text-lg">{{ res.category }}</div>
        <div class="text-bold text-secondary text-lg">{{ res.choice }}</div>
      </li>
    </ul>
    <div class="flex flex-col items-center mt-8">
      <button class="btn btn-primary w-1/3" @click="startOver">Start Over</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    result: Array
  },
  methods: {
    startOver() {
      this.$emit('start-over');
    }
  }
};
</script>
