<script lang="ts" setup>
import type { Terrain } from '@/utils/backend';
import { onMounted } from 'vue';
import L from 'leaflet';

const props = defineProps<{
  terrains: Terrain[]
}>()

onMounted(() => {
  const map = L.map('map').setView([48.8566, 2.3522], 13);

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map);

  props.terrains.forEach(terrain => {
    L.marker([terrain.latitude, terrain.longitude]).addTo(map)
      .bindPopup(`<b>${terrain.nom}</b><br>Surface: ${terrain.surface} m²<br>Prix: ${terrain.prix} €`);
  });
})
</script>

<template>
  <div id="map"></div>
</template>