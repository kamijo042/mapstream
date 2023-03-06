<script setup lang="ts">
import {computed, ref} from "vue";
import {useCounterStore} from "@/stores/counter";

import { GoogleMap, Marker } from "vue3-google-map";

const API_KEY = "AIzaSyBvJcef4p00vXEzUYQI-qsr9RHU2ztkAmE";

const counterStore = useCounterStore();
const count = computed(
  (): number => {
    return counterStore.counter;
  }
);

const doubleCount = computed(
  ():number => {
    return counterStore.doubleCount;
  }
);

const center = { lat: 36.3347951, lng: 136.2960278 };
const zoom = 15;

const onIncrementClick = () => {
  counterStore.incrementCount();
};

const iconOptions = [{
    position: center,
    label: "L",
    title: "黒崎小学校",
  }]

</script>

<template>
  <div>
    <div class="counter">
    <p>現在のポイント: {{ count }}</p>
    <p>現在のポイントのさらに倍: {{ doubleCount }}</p>
    <button v-on:click="onIncrementClick">加算</button>
  </div>

  <div>
    <GoogleMap
    :api-key="API_KEY"
    class="map"
    :center="center"
    :zoom="zoom"
  >
    <Marker
      v-for="option in iconOptions"
      :key="JSON.stringify(option.label)"
      :options="option"
    >
    </Marker>
  </GoogleMap>
  </div>
  </div>
</template>

<style scoped>
.counter {
  font-size: 20px;
}
.map {
  height: calc(100vh - 500px);
  width: 70vw;
  margin-top: 20px;
}

</style>
