<script>
  export default {
    data() {
      return {
        categories: [
          { name: 'Home', option1: '', option2: '', option3: '', option4: ''},
          { name: 'Spouse', option1: '', option2: '', option3: '', option4: ''},
          { name: 'Job', option1: '', option2: '', option3: '', option4: ''},
          { name: 'Car', option1: '', option2: '', option3: '', option4: ''},
        ]
      }
    },
    methods: {
      generateResult() {
        this.$emit('generate', this.categories);
      }
    }
  }
</script>

<template>
  <div class="mash-input">
    <h2>Mash Choices</h2>
    <form @submit.prevent="generateResult">
      <div v-for="(category, index) in categories" :key="index">
        <label>{{ category.name}}</label>
        <input v-model="category.option1" placeholder="Option 1">
        <input v-model="category.option2" placeholder="Option 2">
        <input v-model="category.option3" placeholder="Option 3">
        <input v-model="category.option4" placeholder="Option 4">
      </div>
      <button type="submit">Predict My Future</button>
    </form>
  </div>
</template>

<style scoped>
.mash-input {
  margin: 20px;
}
label {
  display: block;
  margin: 10px 0 5px;
}
input {
  margin: 5px 0;
}
button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #42b983;
  color: white;
  border: none;
  cursor: pointer;
}
</style>