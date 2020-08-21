<template>
  <section class="map-area">

	  <Mapbox 
	 	access-token="pk.eyJ1Ijoic3RzMjQiLCJhIjoiOVB0MlNrbyJ9.aIGsCG9-ISYzL-jNTaz5cg" 
		:map-options="mapOptions" 
		/>

  </section>
</template>

<script>
import Mapbox from 'mapbox-gl-vue'

export default {
	components: { Mapbox },
	data(){
		return {
			// defaults to center of california
			mapOptions: {
				style: 'mapbox://styles/mapbox/outdoors-v11',
				center: [ -119.44944, 37.16611 ],
				zoom: 5
			}
		}
	},
	async asyncData({ params, $content }){
		const newLocation = await $content('releases', this.$route.params.slug)
			.only(['location'])
			.fetch();


		const coordArray = newLocation.location.split(',');

		// Vue.set(this, mapOptions.center, [ coordArray[1], coordArray[0] ]);
		// Vue.set(this, mapOptions.zoom, 7);

		return {
			mapOptions: {
				'center': [ coordArray[1], coordArray[0] ],
				'zoom': 7
			}
		}

		return true
	},
	async fetch(){
		const newLocation = await this.$content('releases', this.$route.params.slug)
			.only(['location'])
			.fetch();

		const coordArray = newLocation.location.split(',');

		this.mapOptions.center = [ coordArray[1], coordArray[0] ];
		this.mapOptions.zoom = 7;
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

<style lang="scss">
	.map-area {
		order: 1;
		background: var(--gray);

		grid-column: 1 / 3;
		grid-row: 1 / 2;
	}

	.map-marker {
		cursor: pointer;
	}
	#map {
		width: 100%;
 		height: 100%;
	}
</style>