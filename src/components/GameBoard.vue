<template>
	<div>
		Player {{ index + 1 }}
		<ul>
			<li class="board__row" v-for="arr in playerBoard.map" :key="arr">
				<ol>
					<li class="board__square" v-for="el in arr" :key="el">
						<p v-if="el">{{ el.terrainTile.type }}</p>
					</li>
				</ol>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
	props: {
		playerBoard: Object,
		index: Number,
	},
	computed: {

	},
};
</script>

<style scoped>
	div {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: space-evenly;
	}
	ol, ul, li {
		padding: 0;
		margin: 0;
	}
	ul {
		border: 5px solid var(--green);
	}
	li {
		/* display: block; */
		border: 1px solid var(--green);
	}
	.board__row {
		display: block;
		width: 100%;
		/* height: 150px; */
	}
	.board__row ol {
		display: flex;
		justify-content: space-evenly;
		align-items: center;
	}
	.board__square {
		width: 16%;
		aspect-ratio: 1 / 1;
	}
</style>