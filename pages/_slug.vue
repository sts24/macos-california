<template>

	<div class="app-container">
		<header class="app-header">macOS California</header>

		<Navigation :NavData="allData" />
	
		<main class="app">
			
			<section class="location-content">
				<h1>{{ systemTitle(article) }}</h1>
				<p>Released on {{ formatDate(article.releaseDate) }}</p>
				<nuxt-content :document="article" />
			</section>

			<Map :location="article.location" />

		</main>

	</div>

</template>

<script>
export default {
	async asyncData ({ $content, params }) {
		const article = await $content('releases', params.slug).fetch();
		const allData = await $content('releases').sortBy('releaseDate', 'asc').fetch();
	
		return { article, allData }
	},
	methods: {
		formatDate(date) {
			const options = { year: 'numeric', month: 'long', day: 'numeric' }
			return new Date(date).toLocaleDateString('en', options)
		},
		systemTitle(article){
			return 'macOS '+ article.version +' '+ article.title;
		}
	}
}
</script>

<style>

.app-header {
  text-align: center;
  font-size: 2em;
  padding: 1rem;
  font-weight: bold;
}

.app {
	display: grid;
	grid-template-columns: 2fr 1fr;
	min-height: 100vh;
}

.location-content {
	background: white;
	order: 2;
}

</style>