<template>
  <div class="home">
  	<div class="header">
  		<img src="../assets/logo.png"><h1>VUE SOME GIFS</h1>
  	</div>
  	<input type="text" class="input" name="query" v-model="query" @keyup="searchGifs" placeholder="Search all of the gifs">
  	<GifGrid v-bind:gifs="searchedGifs" msg="Welcome to Your Vue.js App"/>
  	<button v-if="query" @click="loadMoreGifs">LOAD MORE</button>
    <h1>TRENDING</h1>
    <GifGrid v-bind:gifs="trendingGifs" msg="Welcome to Your Vue.js App"/>
	<button @click="loadMoreTrending">LOAD MORE</button>
  </div>
</template>

<script>
// @ is an alias to /src
import GifGrid from '@/components/GifGrid.vue'


export default {
  name: 'home',
  components: {
    GifGrid
  },
  data() {
  	return {
  		apiUrl: 'http://api.giphy.com/v1/gifs',
        apiKey: '80bfcbf357864cd18518c324f47a7098',
        trendingGifs: null,
        searchedGifs: null,
        searchButton: false,
        query: '',
        limit: 10,
        offset: null
  	}
  },
  methods	: {
  	fetchTrendingGifs: function() {
      const url = `${this.apiUrl}/trending?api_key=${this.apiKey}&limit=${this.limit}`;

      axios.get(url)
        .then(response => this.trendingGifs = response.data.data)
    },

    searchGifs: function() {
	  const url = `${this.apiUrl}/search?api_key=${this.apiKey}&q=${this.query}&limit=${this.limit}`;
	  this.searchButton = true;
	  axios.get(url)
        .then(response => this.searchedGifs = response.data.data)
        .then(console.log(this.searchedGifs))
	},

	loadMoreTrending: function() {
	  this.offset += 10;

	  const url = `${this.apiUrl}/trending?api_key=${this.apiKey}&limit=${this.limit}&offset=${this.offset}`;

	  axios.get(url)
        .then(response => {
        	let i = 0;
	        let loadTrending = response.data.data;
        	for(i = 0; i < this.limit; i++ ) {
        		let addloadTrending = loadTrending[i];
	        	this.trendingGifs.push(addloadTrending);
        	}
        })
	},

	loadMoreGifs: function() {
	  this.offset += 10;

	  const url = `${this.apiUrl}/search?api_key=${this.apiKey}&q=${this.query}&limit=${this.limit}&offset=${this.offset}`;

	  axios.get(url)
        .then(response => {
        	let i = 0;
	        let loadGif = response.data.data;
        	for(i = 0; i < this.limit; i++ ) {
        		let addLoadGif = loadGif[i];
	        	this.searchedGifs.push(addLoadGif);
        	}
        })
	}
  },
  created: function() {
    this.fetchTrendingGifs();
    this.searchGifs();
  }
}


</script>

<style lang="scss">
body {
	background: rgb(18, 18, 18);
	color: #ffffff;
	margin: 30px;
}

h1 {
	color: #ffffff;
	text-align: left;
}

input {
	width: 100%;
	font-size: 3em;
	padding: 5px 10px;
	border-width: 0px;
	margin-bottom: 30px;
	box-sizing: border-box;
}

button {
	border-radius: 0;
	background: #35495e;
	color: #ffffff;
	border-width: 0;
	font-size: 1.5em;
	padding: 15px 20px;
	margin-top: 15px;
	font-weight: bold;
	transition: 0.2s;

	&:hover {
		transition: 0.2s;
		background: #41b883;
		cursor: pointer;
	}
}

.home {
	max-width: 1200px;
	margin: 0 auto;
}

.header {
	display: flex;
	align-items: center;

	img	{
		margin-right: 20px;
		width: 50px;
		height: 50px;
	}
}

@media screen and (max-width: 600px) {
	h1 {
		text-align: center;
	}

	.header {
		justify-content: center;
		margin-bottom: 10px;
	}

	.header h1 {
		font-size: 1.4em;
	}

	.header img {
		margin-right: 10px;
	}

	input {
		margin: 0 auto 15px auto;
		font-size: 1.5em;
		text-align: center;
	}
}
</style>
