<template>

	<div class="app-container">
		<header class="app-header">macOS California</header>

		<Navigation :NavData="allData" />
	
		<main class="app">
			
			<section class="location-content">
				<h1>{{ systemTitle(article) }}</h1>

				<cld-image cloudName="stsmith" :publicId="'macos-california/' + article.slug" crop="fill" width="1200" height="675" />

				<p class="release-date">Released in {{ article.releaseDate }}</p>
				<nuxt-content :document="article" />
			</section>

			<Map :coords="article.location" />

		</main>

	</div>

</template>

<script>
import Cloudinary from "cloudinary-vue";

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

.app-container {
	display: grid;
	grid-template-rows: auto auto 1fr;
	height: 100vh;
	max-height: 100vh;
}

.app-header {
  text-align: center;
  font-size: 2em;
  padding: 1rem;
  font-weight: bold;
}

.app {
	display: grid;
	grid-template-columns: 2fr 1fr;
}

.location-content {
	background: white;
	order: 2;
	display: flex;
	flex-direction: column;
	padding: 2rem;
}

h1 {
	font-size: 2em;
	margin-bottom: 0;
}

p.release-date {
	margin: 1rem 0;
	font-size: 1.5em;
}

.location-content p {
	font-size: 1.25em;
	margin-bottom: 1em;
}

.location-content.cld-image {
	order: -1;
	margin: -2rem -2rem 2rem -2rem;
}

.location-content .cld-image img {
	width: 100%;
	height: auto;
	display: block;
}

</style>