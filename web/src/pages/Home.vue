<script lang="ts" setup>
import ListView from '@/components/ListView.vue';
import MapView from '@/components/MapView.vue';
import { backend } from '@/utils/backend';
import { onMounted, ref } from 'vue';


type Terrain = {
  id: string,
  nom: string,
  latitude: number,
  longitude: number,
  surface: number,
  surfaceConstructible: number,
  prix: number,
  longueurFacade: number,
  orientationFacade: string,
  userId: string
  photos: { id: string, url: string }[],
}

const terrains = ref<Terrain[]>([])
async function getTerrains() {
  const terrainsRes = await backend.terrains.getAll();
  terrains.value = terrainsRes;
}

onMounted(() => {
  getTerrains();
});

const view = ref<'list' | 'map'>('list');
</script>

<template>
  <UContainer class="py-4">
    <div class="mb-4 flex justify-between">
      <UTabs :content="false" v-model="view" :items="{
        list: { label: 'Liste', icon: 'i-lucide-list' },
        map: { label: 'Carte', icon: 'i-lucide-map' },
      }" />
      <UButton label="Ajouter un terrain" icon="i-lucide-plus" to="/terrains/create" />
    </div>

    <ListView v-if="view === 'list'" :terrains="terrains" />
    <MapView v-if="view === 'map' && terrains.length > 0" :terrains="terrains" class="h-200" />
  </UContainer>
</template>