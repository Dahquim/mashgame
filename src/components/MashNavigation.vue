<template>
  <div class="mash-navigation flex gap-4">
    <button class="flex-1 btn btn-primary" @click="$emit('prev')" :disabled="currentStep === 0">Previous</button>
    <button class="flex-1 btn btn-primary" @click="$emit('next')" :disabled="currentStep === totalSteps - 1">Next</button>
    <button class="flex-1 btn btn-secondary" @click="$emit('submit')" :disabled="currentStep !== totalSteps - 1">Submit</button>
  </div>
</template>

<script>
export default {
  props: {
    currentStep: Number,
    totalSteps: Number
  }
};
</script>
