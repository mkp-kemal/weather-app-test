<template>
  <div v-if="props.visible">
  </div>
</template>

<script setup>
import { watch, onMounted } from 'vue';
import maplibregl from 'maplibre-gl';

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

let marker; // Variabel untuk menyimpan marker

onMounted(() => {
  watch(
    () => props.visible,
    (newValue) => {
      if (props.map) {
        const map = props.map;

        if (newValue) {
          addCustomMarker(map);
        } else {
          removeCustomMarker();
        }
      } else {
        console.warn('Map instance is not defined');
      }
    },
    { immediate: true }
  );
});

// Fungsi untuk menambahkan marker
function addCustomMarker(map) {

  // Tambahkan marker ke peta
  marker = new maplibregl.Marker()
    .setLngLat([107.39480047837077, -6.442801051024858])
    .addTo(map);
}

// Fungsi untuk menghapus marker
function removeCustomMarker() {
  if (marker) {
    marker.remove();
    marker = null;
  }
}
</script>
