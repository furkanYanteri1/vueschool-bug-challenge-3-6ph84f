<template>
  <div>
    <figure class="logo">
      <img src="/vueschool-logo.png" alt="VueSchool Logo" />
    </figure>
    <h1>Real-Time Clock</h1>
    <p>{{ formattedTime }}</p>
  </div>
</template>

<script setup>
import { ref, computed, watch, onMounted } from 'vue';

const refreshVar = ref(0);
const interval = 1000; // interval in milliseconds

const refresh = () => {
  refreshVar.value = refreshVar.value % 2 === 0 ? 0 : 1;
};

watch(refreshVar, refresh, { immediate: true });

onMounted(() => {
  // Set up an interval to increase the variable
  setInterval(refresh, interval);
});

const formattedTime = computed(() => {
  const now = Date.now();
  const date = new Date(now);
  const hours = date.getHours().toString().padStart(2, '0');
  const minutes = date.getMinutes().toString().padStart(2, '0');
  const seconds = date.getSeconds().toString().padStart(2, '0');
  const formattedTime = `${hours}:${minutes}:${seconds}`;
  refreshVar.value += 10; // Adjust this based on your actual computation
  return formattedTime;
});
</script>

<style>
.logo {
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 200px;
  height: 45px;
  background-color: white;
  padding: 10px;
  border-radius: 30px;
  overflow: hidden;
  margin: 0 auto;
}

img {
  width: 100%;
}

h1 {
  color: #fc6c94;
}

button {
  margin-bottom: 10px;
  background-color: #00bda7;
  margin: 5px;
}

button:hover {
  background-color: #00b49c;
}

ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 15px;
  place-items: center;
  justify-items: center;
  width: 100%;
}

li {
  color: white;
  background-color: #00c3fc;
  overflow: hidden;
  border-radius: 1rem;
  max-width: 600px;
  width: 100%;
  border-color: white;
  border: 1px;
  position: relative;
}

span {
  display: block;
  background-color: #342c8c;
  padding-top: 10px;
  padding-bottom: 10px;
}

blockquote {
  padding-top: 5px;
  padding-bottom: 10px;
}

p {
  font-weight: bold;
  font-size: 2.5rem;
}

.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.list-leave-active {
  position: absolute;
}
</style>
