<template>
  <div>
    <div class="home">
      <h1>時給計算</h1>
      <label for="monthly-worktime">
        <span>月の平均勤務時間</span>
        <div class="input-container">
          <input
            id="monthly-worktime"
            v-model.number="monthlyWorkTime"
            type="number"
          />
          <span>時間</span>
        </div>
      </label>
      <label for="monthly-wage-average">
        <span>月の平均手取り</span>
        <div class="input-container">
          <input
            id="monthly-wage-average"
            v-model.number="monthlyWageAverage"
            type="number"
          />
          <span>円</span>
        </div>
      </label>
      <label for="yearly-bonus">
        <span>年間賞与額</span>
        <div class="input-container">
          <input id="yearly-bonus" v-model.number="yearlyBonus" type="number" />
          <span>円</span>
        </div>
      </label>
      <button @click="openModal">計算す︎る▶︎</button>
    </div>
    <div v-if="showResultModal" class="modal">
      <div class="modal-content">
        あなたの時給は
        <br />
        {{ hourlyWage }}円です！！
        <br />
        お疲れさまです！！
      </div>
      <div class="modal-background" @click="closeModal" />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    const monthlyWorkTime = 0
    const monthlyWageAverage = 0
    const yearlyBonus = 0
    const showResultModal = false
    return {
      monthlyWorkTime,
      monthlyWageAverage,
      yearlyBonus,
      showResultModal,
    }
  },
  computed: {
    hourlyWage(): number {
      return this.IsWorkTimeValid
        ? Math.floor(this.yearlyWage / 12 / this.monthlyWorkTime)
        : 0
    },
    yearlyWage(): number {
      return this.monthlyWageAverage * 12 + this.yearlyBonus
    },
    IsWorkTimeValid(): boolean {
      return !!this.monthlyWorkTime && this.monthlyWorkTime > 0
    },
  },
  methods: {
    openModal() {
      this.showResultModal = true
    },
    closeModal() {
      this.showResultModal = false
    },
  },
})
</script>

<style>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 80vh;
  max-width: 400px;
  margin: 0 auto;
}

.cost-input {
  margin-bottom: 32px;
}

label {
  min-width: 80%;
}

input {
  padding: 8px;
  height: 28px;
  border: 2px solid #01499b;
  font-size: 20px;
  color: #01499b;
  text-align: right;
}

.input-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

button {
  display: block;
  padding: 12px;
  margin-top: 20px;
  color: #01499b;
  font-size: 20px;
  font-weight: bold;
  border: none;
  letter-spacing: 2px;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 50;
  width: 100%;
  height: 100%;
}

.modal-content {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 100;
  width: 300px;
  height: auto;
  color: #e50011;
  font-size: 28px;
  font-weight: bold;
  transform: translate(-50%, -50%) rotate(-10deg);
}

.modal-background {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(255, 255, 255, 0.8);
}
</style>
