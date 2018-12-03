<template>
  <div class="hello">
    <div class="grid">
		<div class="grid-item" v-for="gif in gifs" v-bind:style="{ 'background-image': 'url(' + gif.images.original.url + ')' }">
			<a :href="gif.bitly_url" target="_blank">
				<div class="grid-info">
					<div class="grid-user">
						<img v-if="gif.user" :src="gif.user.avatar_url" height="35" width="35"><br />
						<span v-if="gif.user">{{ gif.user.display_name }}</span><br />
						Click to View
					</div>
				</div>
			</a>	
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

	a {
		color: #ffffff;
		text-decoration: none;
	}
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

@media screen and (max-width: 600px) {
	.grid-item {
		width: 100%;
		height: 200px;
	}
}

</style>
