<template>
  <div class="container">
    <input
      class="w-100 d-block"
      type="number"
      placeholder="First value"
      v-model="firstValue"
    />
    <input
      class="w-100"
      type="number"
      placeholder="Second value"
      v-model="secondValue"
    />

    <div class="alert alert-danger" role="alert" v-if="error">
      {{ error }}
    </div>

    <div class="alert alert-success" role="alert" v-if="expression">
      {{ expression }} = {{ result }}
    </div>

    <div class="row p-2">
      <div class="col-3 p-1" v-for="(op, index) in operators" :key="index">
        <div @click="action(op)" class="bg-vue-green rounded p-2">{{ op }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      firstValue: null,
      secondValue: null,
      error: null,
      operators: ["+", "-", "*", "/", "%"],
      currentOperator: null,
      result: null,
      expression: null,
    };
  },
  methods: {
    action(op) {
      if (!this.firstValue || !this.secondValue) {
        this.error = "Please provide values first";
        setTimeout(() => {
          this.error = "";
        }, 3000);
        return;
      }
      this.currentOperator = op;
      this.expression = `${this.firstValue} ${this.currentOperator} ${this.secondValue}`;
      this.result = eval(this.expression);
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 600px;
  padding: 10px;
  margin: 0 auto;
  box-sizing: border-box;
}

input {
  margin: 10px 0;
  padding: 10px;
}
.bg-vue-green {
  background: #3fb984;
}

.bg-vue-green:hover {
  cursor: pointer;
  background: #3d5875;
}
</style>
