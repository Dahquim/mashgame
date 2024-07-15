<template>
  <div class="mash-summary my-8">
    <h2 class="text-xl mb-4 text-center">Summary of Your Choices</h2>
    <ul class="mb-8 flex flex-col">
      <li v-for="(category, index) in categories" :key="index">
          <transition-group name="fade" tag="span" class="grid grid-cols-5 my-2 gap-2">
            <div class="font-bold text-primary text-lg">{{ category.name }}:</div>
            <div
              v-for="(option, idx) in category.options"
              :key="idx"
              :class="{ strike: option.eliminated, highlight: !option.eliminated && eliminating }"
              class="shadow p-4 rounded-lg"
            >
                <div class="text-center">
                  {{ option.text }}
                </div>
            </div>
          </transition-group>
      </li>
    </ul>
    <button class="btn btn-primary" @click="$emit('confirm')" :disabled="eliminating">Continue</button>
  </div>
</template>

<script>
export default {
  props: {
    categories: Array,
    eliminating: Boolean
  }
};
</script>