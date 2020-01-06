<template>
	<div id="app">
		<div>
			<h1>Big Doggos</h1>
			<div class="body">
				<div id="note">
					<p>Pick a pupper</p>
				</div>
				<div id="link1">
					<div class="center-item">
						<button v-on:click="puppy">Random Pupper!</button>
					</div>
				</div>
				<div id="link2">
					<div class="center-item">
						<button v-on:click="shibe">Random Shibe!</button>
					</div>
				</div>
				<div id="imgs">
					<got-image v-if="selectedItem" :pic="selectedItem"></got-image>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import GotImg from "./components/GotImg.vue";
export default {
	name: 'app',
	data() {
		return {
			selectedItem: null
		};
	},
	methods: {
		puppy: async function() {
			const getPuppy = await fetch("https://dog.ceo/api/breeds/image/random");
			const getJSON = await getPuppy.json();

			if(getJSON.status === "success") {
				this.selectedItem = getJSON.message;
			}
		},

		shibe: async function() {
			const getShibe = await fetch("https://dog.ceo/api/breed/shiba/images/random");
			const getJSON = await getShibe.json();

			if(getJSON.status === "success") {
				this.selectedItem = getJSON.message;
			}
		}
	},
	components: {
		"got-image": GotImg
	}
}
</script>

<style>
h1 {
	color: pink;
	display: flex;
	justify-content: center;
}

.body {
	display: grid;
	grid-template-columns: auto auto;
	grid-template-rows: auto auto;
	grid-gap: 25px;
	grid-template-areas:
	"n n n"
	"l1 l2 l3"
	". i .";
}

#note {
	grid-area: n;
	align-self: center;
	justify-content: center;
	text-align: center;
}

#link1 {
	grid-area: l1;
}

#link2 {
	grid-area: l2;
}

.center-item {
	display: flex;
	align-items: center;
	justify-content: center;
}

#imgs {
	grid-area: i;
	width: 500px;
	height: 500px;
}
</style>
