<template>
  <div v-if="props.visible">
  </div>
</template>

<script setup>
import { watch, onMounted } from 'vue';

// PROPS DARI PARENT
const props = defineProps({
  visible: {
    type: Boolean,
    required: true,
  },
  map: {
    type: Object,
    required: true,
  },
});

let layerId = 'raster-layer';

onMounted(() => {
  watch(
    () => props.visible,
    (newValue) => {
      if (props.map) {
        const map = props.map;

        if (newValue) {
          addCustomMarker(map);
        } else {
          removeCustomMarker(map);
        }
      } else {
        console.warn('Map instance is not defined');
      }
    },
    { immediate: true }
  );
});

// ADD RASTER LAYER
function addCustomMarker(map) {
  // Tambahkan source raster jika belum ada
  if (!map.getSource(layerId)) {
    map.addSource(layerId, {
      type: 'raster',
      tiles: [
        'https://rami.bmkg.go.id/api/windtemp_get/wafc/WT/snow/850/202405121800/202405131200/1/2/3.png', // DIBLOK BMKG
      ],
      tileSize: 256,
    });
  }

  // Tambahkan layer raster jika belum ada
  if (!map.getLayer(layerId)) {
    map.addLayer({
      id: layerId,
      type: 'raster',
      source: layerId,
      paint: {
        'raster-opacity': 0.7,
      },
    });
  }
}

// REMOVE RASTER LAYER
function removeCustomMarker(map) {
  if (map.getLayer(layerId)) {
    map.removeLayer(layerId);
  }
  if (map.getSource(layerId)) {
    map.removeSource(layerId);
  }
}
</script>
