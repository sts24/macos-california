<template>

  <nav class="app-nav">

	<ul v-if="navData">
		<li v-for="item of navData" :key="item.slug">
			<nuxt-link :to="item.slug" class="release-icon">
				<cld-image cloudName="stsmith" :publicId="'macos-california/' + item.slug" crop="fill" width="200" height="200" />
				<span class="link-number">{{ item.version }}</span>
			</nuxt-link>

			<nuxt-link :to="item.slug" class="release-title" aria-hidden="true">
				{{ item.title }}
			</nuxt-link>
		</li>
	</ul>

  </nav>

</template>

<script>
import Cloudinary from "cloudinary-vue";

export default {
	data(){
		return {
			navData: []
		}
	},
	async fetch(){
		this.navData = await this.$content('releases')
			.only(['title', 'slug', 'version'])
			.sortBy('releaseDate', 'asc')
			.fetch();
	}
}
</script>

<style lang="scss">
	.app-nav {
		padding: 1rem;
		overflow-x: scroll;
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


	.release-icon {
		text-decoration: none;

		display: grid;
		justify-content: center;
		align-items: center;
		width: 80px;
		height: 80px;
		margin: 0 0.5rem;

		@media (min-width: 768px){
			width: 100px;
			height: 100px;
		}
	}

		.release-icon .cld-image {
			z-index: 1;
			grid-column: 1 / 2;
			grid-row: 1 / 2;
			border-radius: 100%;
			overflow: hidden;
		}

			.release-icon .cld-image img {
				display: block;
				width: 100%;
				height: 100%;
			}

			.release-icon.active .cld-image {
				box-shadow: 0 0 0 4px var(--link);
			}

	.link-number {
		color: white;
		font-size: 1.25em;
		z-index: 2;
		grid-column: 1 / 2;
		grid-row: 1 / 2;
		text-align: center;
		text-shadow: 0 0 5px black;

		@media (min-width: 768px){
			font-size: 1.5em;
		}
	}




	.release-title {
		text-decoration: none;
		display: block;
		margin-top: 0.5em;
		text-align: center;
		font-weight: bold;
		color: black;
		font-size: 0.875rem;

		@media (min-width: 768px){
			font-size: 1rem;
		}
	}

</style>