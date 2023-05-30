<script setup lang="ts">
import { Cartesian3, Ion, Math, Viewer, createOsmBuildings, createWorldTerrainAsync } from 'cesium'
import 'cesium/Build/Cesium/Widgets/widgets.css'

// Your access token can be found at: https://cesium.com/ion/tokens.
// This is the default access token
Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJkMDc3MzE1MC1lZWMwLTQzNWEtYTVhZS0yZTllNDA4M2U2YjciLCJpZCI6MTE2MDc4LCJpYXQiOjE2NjkzNjU5NDN9.Wo46xHPOIeZR6EQLJ7bstGKVHeTUyzYi2cPapU8-tOs'
onMounted(async () => {
  // Initialize the Cesium Viewer in the HTML element with the `cesiumContainer` ID.
  // Create Cesium World Terrain with default settings
  try {
    const terrainProvider = await createWorldTerrainAsync()
    const viewer = new Viewer('cesiumContainer', {
      terrainProvider,
    })

    // Add Cesium OSM Buildings, a global 3D buildings layer.
    viewer.scene.primitives.add(createOsmBuildings())

    // Fly the camera to San Francisco at the given longitude, latitude, and height.
    viewer.camera.flyTo({
      destination: Cartesian3.fromDegrees(122.15512, 29.95867, 10000),
      orientation: {
        heading: Math.toRadians(0),
        pitch: Math.toRadians(-90.0),
      },
    })
  }
  catch (error) {
    console.log(error)
  }
})
</script>

<template>
  <div id="cesiumContainer" />
</template>
