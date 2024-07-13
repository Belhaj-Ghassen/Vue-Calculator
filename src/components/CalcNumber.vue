<template>
  <div class="container mt-5" >
    <div class="row justify-content-center">
      <div class="col-md-6 col-lg-4">
        <div class="card">
          <div class="card-header bg-success text-white text-center">
            <h3>Vue Calculator</h3>
          </div>
          <div class="card-body p-2">
            <div class="form-control form-control-lg mb-3 text-end bg-dark text-white">
              {{ current }}
            </div>
            <div class="row g-2">
              <div class="col-6 col-sm-3">
                <button class="btn btn-light w-100" @click="percent">%</button>
              </div>
              <div class="col-6 col-sm-3">
                <button class="btn btn-light w-100" @click="squareRoot">√</button>
              </div>
              <div class="col-6 col-sm-3">
                <button class="btn btn-light w-100" @click="clearEntry">CE</button>
              </div>
              <div class="col-6 col-sm-3">
                <button class="btn btn-light w-100" @click="clear">C</button>
              </div>

              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(7)">7</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(8)">8</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(9)">9</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(4)">4</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(5)">5</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(6)">6</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(1)">1</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(2)">2</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(3)">3</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendNumber(0)">0</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-secondary w-100" @click="appendDecimal()">.</button>
              </div>
              <div class="col-4 col-sm-3">
                <button class="btn btn-light w-100" @click="compute">=</button>
              </div>
              <div class="col-6 col-sm-3">
                <button class="btn btn-light w-100" @click="chooseOperation('+')">+</button>
              </div>
              <div class="col-6 col-sm-3">
                <button class="btn btn-light w-100" @click="chooseOperation('-')">-</button>
              </div>
              <div class="col-6 col-sm-3">
                <button class="btn btn-light w-100" @click="chooseOperation('x')">x</button>
              </div>
              <div class="col-6 col-sm-3">
                <button class="btn btn-light w-100" @click="chooseOperation('÷')">÷</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      previous: '',
      operation: null
    };
  },
  methods: {
    appendNumber(number) {
      if (this.current.includes('.') && number === '.') return;
      this.current = `${this.current}${number}`;
    },
    appendDecimal() {
      if (this.current.includes('.')) return;
      this.current = `${this.current}.`;
    },
    clear() {
      this.current = '';
      this.previous = '';
      this.operation = null;
    },
    clearEntry() {
      this.current = '';
    },
    chooseOperation(operation) {
      if (this.current === '') return;
      if (this.previous !== '') {
        this.compute();
      }
      this.operation = operation;
      this.previous = this.current;
      this.current = '';
    },
    compute() {
      let computation;
      const prev = parseFloat(this.previous);
      const curr = parseFloat(this.current);
      if (isNaN(prev) || isNaN(curr)) return;
      switch (this.operation) {
        case '+':
          computation = prev + curr;
          break;
        case '-':
          computation = prev - curr;
          break;
        case 'x':
          computation = prev * curr;
          break;
        case '÷':
          computation = prev / curr;
          break;
        default:
          return;
      }
      this.current = computation;
      this.operation = null;
      this.previous = '';
    },
    percent() {
      if (this.current === '') return;
      this.current = `${parseFloat(this.current) / 100}`;
    },
    squareRoot() {
      if (this.current === '') return;
      this.current = `${Math.sqrt(parseFloat(this.current))}`;
    }
  }
};
</script>
<style>
body {
  background-color: #20ac6d	;
}
</style>
