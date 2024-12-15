<script setup>
import { watch } from 'vue';

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

// SET MAP FROM PARENT
watch(
  () => props.visible,
  (newValue) => {
    if (props.map) {
      const map = props.map;

      if (map.loaded()) {
        onMapReady(map, newValue);
      } else {
        map.once('load', () => {
          onMapReady(map, newValue);
        });
      }
    } else {
      console.warn('Map instance is not defined');
    }
  },
  { immediate: true }
);

const layer = {
  id: 'line-layer',
  type: 'line',
  source: {
    type: 'geojson',
    data: {
      type: 'FeatureCollection',
      features: [
        {
          type: 'Feature',
          geometry: {
            type: 'LineString',
            coordinates: [
              [98.10100725226522, 3.8251479723679154],
              [100.78211917651106, 3.4730858909893954],
              [104.80378706288087, 0.9351724663382726],
              [107.62601014103257, -1.6751036732165119],
              [110.87156668091097, -2.662162045378949],
            ],
          },
          properties: { nama: 'Jalur Lintas Negara', lineColor: 'yellow' },
        },
      ],
    },
  },
}

function onMapReady(map, visible) {
  if (visible) {
    // Tambahkan layer jika belum ada
    if (!map.getLayer(layer.id)) {
      map.addLayer({
        ...layer,
        paint: {
          'line-color': layer.source.data.features[0].properties.lineColor,
          'line-width': 4,
        },
      });
    }
  } else {
    if (map.getLayer(layer.id)) {
      map.removeLayer(layer.id);
      map.removeSource(layer.id);
    }
  }
}
</script>
