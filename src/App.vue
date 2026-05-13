<template>
  <main class="page">
    <h1 class="title">SPLI<br>TTER</h1>

    <section class="calculator-card" aria-label="Tip calculator">
      <div class="input-panel">
        <label class="field-label" for="bill">Bill</label>
        <div class="input-wrap">
          <span class="input-icon">$</span>
          <input
            id="bill"
            v-model="bill"
            class="number-input"
            type="number"
            min="0"
            step="0.01"
            placeholder="0"
          >
        </div>

        <p class="field-label">Select Tip %</p>
        <div class="tip-grid">
          <button
            v-for="tip in presetTips"
            :key="tip"
            type="button"
            class="tip-btn"
            :class="{ active: selectedTip === tip }"
            @click="selectTip(tip)"
          >
            {{ tip }}%
          </button>

          <input
            v-model="customTip"
            class="tip-custom"
            type="number"
            min="0"
            step="0.1"
            placeholder="Custom"
            aria-label="Custom tip percentage"
            @input="handleCustomTip"
          >
        </div>

        <div class="people-header">
          <label class="field-label" for="people">Number of People</label>
          <span v-if="showPeopleError" class="error-text">Can't be zero</span>
        </div>
        <div class="input-wrap" :class="{ invalid: showPeopleError }">
          <span class="input-icon">👤</span>
          <input
            id="people"
            v-model="people"
            class="number-input"
            type="number"
            min="1"
            step="1"
            placeholder="0"
          >
        </div>
      </div>

      <div class="result-panel">
        <div class="result-row">
          <div>
            <p class="result-label">Tip Amount</p>
            <p class="result-sub">/ person</p>
          </div>
          <p class="result-value">${{ tipPerPerson }}</p>
        </div>

        <div class="result-row">
          <div>
            <p class="result-label">Total</p>
            <p class="result-sub">/ person</p>
          </div>
          <p class="result-value">${{ totalPerPerson }}</p>
        </div>

        <button
          type="button"
          class="reset-btn"
          :disabled="!hasInput"
          @click="resetCalculator"
        >
          RESET
        </button>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      bill: '',
      people: '',
      selectedTip: 15,
      customTip: '',
      presetTips: [5, 10, 15, 25, 50]
    }
  },
  computed: {
    parsedBill() {
      const value = Number(this.bill)
      return Number.isFinite(value) && value > 0 ? value : 0
    },
    parsedPeople() {
      const value = Number(this.people)
      return Number.isFinite(value) && value > 0 ? value : 0
    },
    activeTipPercent() {
      const custom = Number(this.customTip)

      if (this.customTip !== '' && Number.isFinite(custom) && custom >= 0) {
        return custom
      }

      return this.selectedTip
    },
    showPeopleError() {
      return this.people !== '' && this.parsedPeople === 0
    },
    tipPerPerson() {
      if (this.parsedBill === 0 || this.parsedPeople === 0) {
        return '0.00'
      }

      const tipAmount = this.parsedBill * (this.activeTipPercent / 100)
      return (tipAmount / this.parsedPeople).toFixed(2)
    },
    totalPerPerson() {
      if (this.parsedBill === 0 || this.parsedPeople === 0) {
        return '0.00'
      }

      const tipAmount = this.parsedBill * (this.activeTipPercent / 100)
      const total = this.parsedBill + tipAmount
      return (total / this.parsedPeople).toFixed(2)
    },
    hasInput() {
      return this.bill !== '' || this.people !== '' || this.customTip !== '' || this.selectedTip !== 15
    }
  },
  methods: {
    selectTip(tip) {
      this.selectedTip = tip
      this.customTip = ''
    },
    handleCustomTip() {
      if (this.customTip !== '') {
        this.selectedTip = 0
      }
    },
    resetCalculator() {
      this.bill = ''
      this.people = ''
      this.selectedTip = 15
      this.customTip = ''
    }
  }
}
</script>

<style>
:root {
  --bg: #c5e4e7;
  --card: #ffffff;
  --panel: #00474b;
  --ink: #3c6b6f;
  --ink-strong: #00474b;
  --muted: #7f9c9f;
  --accent: #26c2ad;
  --accent-soft: #9fe8df;
  --danger: #e17457;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
}

#app {
  min-height: 100vh;
  font-family: 'Trebuchet MS', 'Segoe UI', sans-serif;
  background: radial-gradient(circle at top left, #d8f3f5, var(--bg));
}

.page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 2.4rem;
  padding: 2rem 1rem;
}

.title {
  margin: 0;
  font-size: 1.4rem;
  letter-spacing: 0.5rem;
  line-height: 1.4;
  color: var(--ink-strong);
  text-align: center;
}

.calculator-card {
  width: min(920px, 100%);
  background: var(--card);
  border-radius: 1.5rem;
  padding: 1.8rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.6rem;
  box-shadow: 0 1rem 2.2rem rgba(0, 71, 75, 0.15);
}

.input-panel {
  padding: 0.7rem;
}

.field-label {
  margin: 0 0 0.45rem;
  font-size: 0.92rem;
  font-weight: 700;
  color: var(--ink);
}

.people-header {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
}

.error-text {
  font-size: 0.86rem;
  font-weight: 700;
  color: var(--danger);
}

.input-wrap {
  position: relative;
  margin-bottom: 1.5rem;
}

.input-wrap.invalid .number-input {
  border: 2px solid var(--danger);
}

.input-icon {
  position: absolute;
  left: 0.8rem;
  top: 50%;
  transform: translateY(-50%);
  font-size: 1rem;
  color: var(--muted);
}

.number-input,
.tip-custom {
  width: 100%;
  border: 2px solid transparent;
  border-radius: 0.35rem;
  background: #f3f8fb;
  color: var(--ink-strong);
  font-size: 1.45rem;
  font-weight: 700;
  text-align: right;
  padding: 0.5rem 0.75rem;
  outline: none;
}

.number-input {
  padding-left: 2rem;
}

.number-input:focus,
.tip-custom:focus {
  border-color: var(--accent);
}

.number-input::placeholder,
.tip-custom::placeholder {
  color: #9ebbbd;
}

.tip-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 0.8rem;
  margin-bottom: 1.5rem;
}

.tip-btn {
  border: none;
  border-radius: 0.35rem;
  background: var(--panel);
  color: #fff;
  font-size: 1.35rem;
  font-weight: 700;
  padding: 0.52rem 0.4rem;
  cursor: pointer;
  transition: background-color 0.2s ease, color 0.2s ease;
}

.tip-btn:hover,
.tip-btn.active {
  background: var(--accent-soft);
  color: var(--panel);
}

.tip-custom {
  font-size: 1.2rem;
}

.result-panel {
  background: var(--panel);
  border-radius: 0.9rem;
  padding: 2.2rem 1.8rem 1.8rem;
  display: flex;
  flex-direction: column;
  gap: 1.65rem;
}

.result-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.result-label {
  margin: 0;
  color: #fff;
  font-size: 0.92rem;
  font-weight: 700;
}

.result-sub {
  margin: 0.24rem 0 0;
  color: var(--muted);
  font-size: 0.8rem;
}

.result-value {
  margin: 0;
  color: var(--accent);
  font-size: clamp(1.7rem, 5vw, 2.9rem);
  font-weight: 700;
}

.reset-btn {
  margin-top: auto;
  border: none;
  border-radius: 0.35rem;
  padding: 0.75rem;
  background: var(--accent);
  color: var(--panel);
  font-size: 1.15rem;
  font-weight: 700;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.reset-btn:hover:not(:disabled) {
  background: var(--accent-soft);
}

.reset-btn:disabled {
  background: #0d686d;
  color: #83a9ab;
  cursor: not-allowed;
}

@media (max-width: 840px) {
  .calculator-card {
    grid-template-columns: 1fr;
    max-width: 560px;
    padding: 1.3rem;
  }

  .result-panel {
    min-height: 260px;
    padding: 1.65rem 1.35rem 1.35rem;
  }
}

@media (max-width: 500px) {
  .tip-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
</style>
