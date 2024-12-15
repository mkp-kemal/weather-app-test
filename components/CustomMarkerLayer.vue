<template>
  <div v-if="props.visible">
  </div>
</template>

<script setup>
import { watch, onMounted } from 'vue';
import maplibregl from 'maplibre-gl';
import logo from '../assets/circlegeo.png';

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

let marker;

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

// ADD MARKER
function addCustomMarker(map) {
  marker = new maplibregl.Marker({
    element: createCustomMarkerElement(),
  })
    .setLngLat([112.4748020190462, -7.493302647866955])
    .addTo(map);
}

const createCustomMarkerElement = () => {
  const img = document.createElement('img');
  img.src = logo;
  img.style.width = '80px';
  img.style.height = '80px';
  img.style.cursor = 'pointer';
  return img;
};

function removeCustomMarker() {
  if (marker) {
    marker.remove();
    marker = null;
  }
}
</script>
