<template>
  <div class="hello">
    <div class="grid">
		<div class="grid-item" v-for="gif in gifs" v-bind:style="{ 'background-image': 'url(' + gif.images.original.url + ')' }">
			<div class="grid-info">
				<span v-if="gif.user">{{ gif.user.display_name }}</span><br />
				Click to Vue
			</div>
		</div>
	</div>
  </div>
</template>

<script>
export default {
  name: 'GifGrid',
  props: {
    msg: String,
    gifs: Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.grid {
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
}

.grid-item {
	background-position: center;
	background-size: cover;
	width: 220px;
	height: 180px;
	margin: 10px;
}

.grid-info {
	height: 100%;
	color: #ffffff;
	background: rgba(0,0,0,0.7);
	display: flex;
	align-items: center;
	justify-content: center;
	opacity: 0;
	transition: 0.3s;
	font-size: 12px;
	flex-wrap: wrap;

	&:hover {
		opacity: 1;
		transition: 0.3s;
	}
}

</style>
