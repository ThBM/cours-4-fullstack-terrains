<script lang="ts" setup>
import type { Terrain } from '@/utils/backend';

const props = defineProps<{
  terrains: Terrain[]
}>()

</script>

<template>
  <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
    <UCard v-for="terrain in props.terrains" :key="terrain.id" :ui="{ header: 'p-0 sm:p-0' }">
      <template #header>
        <div class="h-50 bg-gray-200">
          <img v-if="terrain.photos.length > 0" :src="terrain.photos[0]!.url" class="h-full w-full object-cover" />
        </div>
      </template>

      <div class="space-y-2">
        <h3 class="font-bold text-lg">{{ terrain.nom }}</h3>
        <p><strong>Surface :</strong> {{ terrain.surface }} m²</p>
        <p><strong>Surface Constructible :</strong> {{ terrain.surfaceConstructible }} m²</p>
        <p><strong>Prix :</strong> {{ terrain.prix }} €</p>
        <p><strong>Longueur de la Façade :</strong> {{ terrain.longueurFacade }} m</p>
        <p><strong>Orientation de la Façade :</strong> {{ terrain.orientationFacade }}</p>
      </div>
    </UCard>
  </div>
</template>