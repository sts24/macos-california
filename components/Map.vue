<template>
  <section class="map-area">

	  <Mapbox 
	 	access-token="pk.eyJ1Ijoic3RzMjQiLCJhIjoiOVB0MlNrbyJ9.aIGsCG9-ISYzL-jNTaz5cg" 
		:map-options="{ 
			style: 'mapbox://styles/mapbox/outdoors-v11',
			center: [-119.637801, 37.731437 ], // long and lat
			zoom: 11,
			}" 
		/>


  </section>
</template>

<script>
import Mapbox from 'mapbox-gl-vue'

export default {
	components: { Mapbox },
	props: ['location'],
	head() {
		return {
			script: [
				{
					'src': 'https://api.mapbox.com/mapbox-gl-js/v1.11.1/mapbox-gl.js'
				}
			],
			link: [
				{ 
					'href': 'https://api.mapbox.com/mapbox-gl-js/v1.11.1/mapbox-gl.css',
					'rel': 'stylesheet'
				}
			]
		}
	}
}


</script>

<style>
	.map-area {
		order: 1;
		background: gray;
	}

	#map {
		width: 100%;
 		height: 100%;
	}
</style>