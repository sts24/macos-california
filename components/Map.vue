<template>
  <section class="map-area">

	  <Mapbox 
	 	access-token="pk.eyJ1Ijoic3RzMjQiLCJhIjoiOVB0MlNrbyJ9.aIGsCG9-ISYzL-jNTaz5cg" 
		:map-options="{ 
			style: 'mapbox://styles/mapbox/outdoors-v11',
			center: coordsFormatted, // long and lat
			zoom: 11,
			}" 
		/>


  </section>
</template>

<script>
import Mapbox from 'mapbox-gl-vue'

export default {
	components: { Mapbox },
	props: ['coords'],
	computed: {
		coordsFormatted: function(){
			const coordArray = this.coords.split(',');
			return [ coordArray[1], coordArray[0] ];
		}
	},
	head() {
		return {
			script: [{
				'src': 'https://api.mapbox.com/mapbox-gl-js/v1.11.1/mapbox-gl.js'
			}],
			link: [{ 
				'href': 'https://api.mapbox.com/mapbox-gl-js/v1.11.1/mapbox-gl.css',
				'rel': 'stylesheet'
			}]
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