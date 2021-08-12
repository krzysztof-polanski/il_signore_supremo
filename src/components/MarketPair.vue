<template>
	<li>
		<h3>{{ pair.terrainTile.type }}</h3>
		<img :src="getImgUrl(pair.terrainTile.type)" alt="">
		<!-- <h4>{{ pair.token }}</h4> -->
	</li>
</template>

<script>
	

export default {
  props: {
    pair: Object,
  },
	methods: {
		getImgUrl(terrainType) {
			console.log(terrainType)
			let images = require.context('../assets/', false, /\.jpg$/);
			return images('./' + terrainType + ".jpg");
		},
	},
}
</script>

<style scoped>
	img {
		width: 20vw;
		aspect-ratio: 1 / 1;
	}
	h3 {
		text-transform: uppercase;
	}
</style>