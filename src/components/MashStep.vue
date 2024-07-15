<template>
  <div class="mash-step my-8">
    <h2 class="text-xl mb-4 text-center">Step {{ stepNumber }}: {{ category.name }}</h2>
    <ul class="flex flex-col gap-4">
      <li v-for="(option, index) in category.options" :key="index">
        <input class="input input-bordered w-full" v-model="option.text" placeholder="Enter an option" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    category: Object,
    stepNumber: Number
  }
};
</script>