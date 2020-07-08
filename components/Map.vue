<template>
  <section class="map-area">

	  {{ location }}

  </section>
</template>

<script>
export default {
	props: ['location']
}
</script>

<style>
	.map-area {
		order: 1;
		background: gray;
	}
</style>