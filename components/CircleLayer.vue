<script setup>
import { watch } from 'vue';

// PROPS FROM PARENT
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
  id: 'circle-layer',
  name: 'Circle',
  visible: true,
  type: 'circle',
  source: {
    type: 'geojson',
    data: {
      type: 'FeatureCollection',
      features: [
        {
          type: 'Feature',
          geometry: {
            coordinates: [
              120.07270882054462,
              -1.6115571819790233
            ],
            type: "Point"
          },
          properties: { nama: 'Circle Marker', radius: 10 },
        },
      ],
    },
  },
}

// LOAD MAP WITH LAYER
function onMapReady(map, visible) {
  if (visible) {
    if (!map.getLayer(layer.id)) {
      map.addLayer({
        ...layer,
        paint: {
          'circle-radius': layer.source.data.features[0].properties.radius,
          'circle-color': '#0000FF',
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