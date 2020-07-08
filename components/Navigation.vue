<template>
  <nav class="app-nav">

	  <ul>
		  <li v-for="item of NavData" :key="item.slug">
			  <nuxt-link :to="item.slug">{{ item.title }}</nuxt-link>
		  </li>
	  </ul>

  </nav>
</template>

<script>
export default {
	props: ['NavData']
}
</script>

<style>
	.app-nav {
		padding: 1rem;
	}

	.app-nav > ul {
		list-style: none;
		padding: 0;
		margin: 0;
		display: flex;
		justify-content: space-between;
	}

	.app-nav > ul > li {
		margin: 0;
		padding: 0;
	}
	
</style>