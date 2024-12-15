<script setup>
import { onMounted, ref, watch } from 'vue';
import maplibregl from 'maplibre-gl';
import 'maplibre-gl/dist/maplibre-gl.css';
import LineLayer from './LineLayer.vue';
import CircleLayer from './CircleLayer.vue';
import PolygonLayer from './PolygonLayer.vue';
import DefaultMarkerLayer from './DefaultMarkerLayer.vue';
import CustomMarkerLayer from './CustomMarkerLayer.vue';
import VectorTilesLayer from './VectorTilesLayer.vue';

const map = ref(null);
const lineVisible = ref(false);
const circleVisible = ref(false);
const polygonVisible = ref(false);
const defaultMarkerVisible = ref(false);
const customMarkerVisible = ref(false);
const tilesMarkerVisible = ref(false);

onMounted(() => {
  // SET MAP MAPLIBRE GL
  map.value = new maplibregl.Map({
    container: 'map',
    style: 'https://api.maptiler.com/maps/streets/style.json?key=cQX2iET1gmOW38bedbUh',
    center: [120.07270882054462, -1.6115571819790233],
    zoom: 3,
  });

  // SET PIP UP
  map.value.on('load', () => {
    getPopup();
  });
});

function getPopup() {
  if (!map.value) return;

  const popup = new maplibregl.Popup({
    closeButton: false,
    closeOnClick: false,
  });

  map.value.on('mousemove', ['line-layer', 'circle-layer', 'polygon-layer'], (e) => {
    if (e.features && e.features.length > 0) {
      const mousePosition = e.lngLat;

      //VIEW POPUP
      popup
        .setLngLat(mousePosition)
        .setHTML(`
          <div class="popup-content">
            <p class="popup-header">2024-12-15 09:18:16.988 UTC</p>
            <p class="popup-title">Coordinates</p>
            <p class="popup-lat-lon">Latitude: ${mousePosition.lat}</p>
            <p class="popup-lat-lon">Longitude: ${mousePosition.lng}</p>
            <button class="popup-button">Detailed Forecast</button>
          </div>
        `)
        .addTo(map.value);
    }
  });

  map.value.on('mouseleave', ['line-layer', 'circle-layer', 'polygon-layer'], () => {
    popup.remove();
  });
}
</script>

<template>
  <div class="relative w-full h-screen">
    <!-- MAP -->
    <div id="map" class="w-full h-[500px]"></div>

    <!-- LAYERS CONTROL -->
    <div class="absolute top-2 left-2 bg-white p-3 rounded shadow">
      <div>
        <label>
          <input type="checkbox" v-model="lineVisible" /> Line Layer
        </label>
        <div>
          <label>
            <input type="checkbox" v-model="circleVisible" /> Circle Layer
          </label>
        </div>
        <div>
          <label>
            <input type="checkbox" v-model="polygonVisible" /> Polygon Layer
          </label>
        </div>
        <div>
          <label>
            <input type="checkbox" v-model="defaultMarkerVisible" /> Default Marker Layer
          </label>
        </div>
        <div>
          <label>
            <input type="checkbox" v-model="customMarkerVisible" /> Custom Marker Layer
          </label>
        </div>
        <div>
          <label>
            <input type="checkbox" v-model="tilesMarkerVisible" /> Vector Tiles Layer
          </label>
        </div>
      </div>
    </div>

    <!-- LAYERS -->
    <LineLayer :visible="lineVisible" :map="map" />
    <CircleLayer :visible="circleVisible" :map="map" />
    <PolygonLayer :visible="polygonVisible" :map="map" />
    <DefaultMarkerLayer :visible="defaultMarkerVisible" :map="map" />
    <CustomMarkerLayer :visible="customMarkerVisible" :map="map" />
    <VectorTilesLayer :visible="tilesMarkerVisible" :map="map" />
  </div>
</template>

<style scoped>
.custom-popup {
  max-width: 300px;
  padding: 10px;
  font-family: Arial, sans-serif;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.popup-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.popup-header {
  font-weight: bold;
  color: #333;
  margin-bottom: 5px;
}

.popup-title {
  font-size: 14px;
  color: #444;
  margin-bottom: 5px;
}

.popup-lat-lon {
  font-size: 12px;
  color: #555;
}

.popup-button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 5px 10px;
  margin-top: 10px;
  border-radius: 4px;
  cursor: pointer;
}

.popup-button:hover {
  background-color: #0056b3;
}
</style>