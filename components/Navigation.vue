<template>
  <nav class="app-nav">

	<ul>
		<li v-for="item of NavData" :key="item.slug">
			<nuxt-link :to="item.slug">
				<span class="link-number">{{ item.version }}</span>
				<span class="link-label">{{ item.title }}</span>
			</nuxt-link>
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
	
	.app-nav > ul > li > a {
		display: block;
		text-decoration: none;
	}

	.app-nav > ul > li > a.nuxt-link-active .link-number {
		outline: 3px solid blue;
	}

	.link-number {
		display: flex;
		width: 100px;
		height: 100px;
		background-color: gray;
		justify-content: center;
		align-items: center;
		color: black;
		font-size: 1.5em;
	}

	.link-label {
		display: block;
		margin-top: 0.5em;
		text-align: center;
		font-weight: bold;
		color: black;
	}

</style>