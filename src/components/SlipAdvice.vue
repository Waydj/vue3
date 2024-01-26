<script setup>
import { ref } from "vue";
import axios from "axios";

const advice = ref(null);

const fetchAdvice = async () => {
  try {
    const response = await axios.get("https://api.adviceslip.com/advice", {
      headers: { Accept: "application/json" },
    });
    advice.value = response.data.slip.advice;
  } catch (error) {
    console.error("Error fetching advice:", error);
  }
};
</script>

<template>
  <div class="advice-container">
    <h2 class="advice-title">Slip advice</h2>
    <button @click="fetchAdvice" class="advice-button">Get Slip Advice</button>
    <div v-if="advice" class="advice">
      {{ advice }}
    </div>
  </div>
</template>

<style scoped>
.advice-container {
  max-width: 600px;
  margin: 50px auto;
}

.advice-title {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
}

.advice-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.advice-button:hover {
  background-color: #45a049;
}

.advice {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 15px;
  margin-top: 20px;
  background-color: #f9f9f9;
  color: #333;
}
</style>
