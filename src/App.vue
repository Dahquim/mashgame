<template>
  <div id="app" class="flex flex-col w-2/3 m-auto">
    <h1 class="text-3xl text-primary">MASH Game</h1>
    <MashStep
      v-if="!result && !showSummary"
      :category="categories[currentStep]"
      :stepNumber="currentStep + 1"
    />
    <MashNavigation
      v-if="!result && !showSummary"
      :currentStep="currentStep"
      :totalSteps="categories.length"
      @prev="prevStep"
      @next="nextStep"
      @submit="showSummary = true"
    />
    <MashSummary
      v-if="showSummary && !result"
      :categories="categories"
      @confirm="startElimination"
    />
    <MashResult
      v-if="result"
      :result="result"
      @start-over="startOver"
    />
  </div>
</template>

<script>
import MashStep from './components/MashStep.vue';
import MashNavigation from './components/MashNavigation.vue';
import MashSummary from './components/MashSummary.vue';
import MashResult from './components/MashResult.vue';

export default {
  name: 'App',
  components: {
    MashStep,
    MashNavigation,
    MashSummary,
    MashResult
  },
  data() {
    return {
      currentStep: 0,
      categories: [
        { name: 'Home', options: [{ text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }] },
        { name: 'Spouse', options: [{ text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }] },
        { name: 'Job', options: [{ text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }] },
        { name: 'Car', options: [{ text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }] }
      ],
      showSummary: false,
      result: null,
      eliminating: false,
    };
  },
  methods: {
    prevStep() {
      if (this.currentStep > 0) {
        this.currentStep--;
      }
    },
    nextStep() {
      if (this.currentStep < this.categories.length - 1) {
        this.currentStep++;
      }
    },
    async startElimination() {
      this.eliminating = true;
      const selectedNumber = Math.floor(Math.random() * 10) + 1; // Random number between 1 and 10
      console.log('Selected Number:', selectedNumber);
      await this.eliminateOptions(selectedNumber);
      this.eliminating = false;
      this.generateResult();
    },
    async eliminateOptions(number) {
      let counter = 0;
      while (this.categories.some(category => category.options.filter(option => !option.eliminated).length > 1)) {
        for (const category of this.categories) {
          if (category.options.filter(option => !option.eliminated).length === 1) {
            continue; // Skip if only one option left
          }
          for (const option of category.options) {
            if (!option.eliminated) {
              counter++;
              if (counter === number) {
                option.eliminated = true;
                console.log(`Eliminated ${option.text} from ${category.name}`);
                counter = 0;
                await this.$nextTick();
                await new Promise(resolve => setTimeout(resolve, 500)); // Animation delay
              }
              if (category.options.filter(option => !option.eliminated).length === 1) break;
            }
          }
        }
      }
    },
    generateResult() {
      this.result = this.categories.map(category => {
        const remainingOption = category.options.find(option => !option.eliminated);
        return {
          category: category.name,
          choice: remainingOption ? remainingOption.text : 'None'
        };
      });
      console.log('Generated Result:', this.result);
    },
    startOver() {
      this.currentStep = 0;
      this.categories = [
        { name: 'Home', options: [{ text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }] },
        { name: 'Spouse', options: [{ text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }] },
        { name: 'Job', options: [{ text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }] },
        { name: 'Car', options: [{ text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }, { text: '', eliminated: false }] }
      ];
      this.showSummary = false;
      this.result = null;
      this.eliminating = false;
    }
  }
};
</script>