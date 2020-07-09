<template>
  <section class="map-area">

	  {{ location }}

	  <MglMap :accessToken="accessToken" :mapStyle="mapStyle" />

  </section>
</template>

<script>
import Mapbox from "mapbox-gl";
import { MglMap } from "vue-mapbox";

export default {
	props: ['location'],
	data() {
		return {
			accessToken: 'pk.eyJ1Ijoic3RzMjQiLCJhIjoiOVB0MlNrbyJ9.aIGsCG9-ISYzL-jNTaz5cg', // your access token. Needed if you using Mapbox maps
			mapStyle: MAP_STYLE // your map style
		};
	},
	created() {
		// We need to set mapbox-gl library here in order to use it in template
		this.mapbox = Mapbox;
	}
}


</script>

<style>
	@import "https://api.tiles.mapbox.com/mapbox-gl-js/v0.53.0/mapbox-gl.css";

	.map-area {
		order: 1;
		background: gray;
	}
</style>