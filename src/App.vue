<template>
	<div id="app">
		<div>
			<h1>I love you</h1>
			<div class="body">
				<div id="note">
					<p>This website has been made specifically for you.</p>
					<p>Certain sections are for your eyes only. The password is our anniversary, use my date format.</p>
					<p>I hope this helps with the big sads.</p>
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
			const getShibe = await fetch("http://shibe.online/api/shibes?count=1&urls=true&httpsUrls=true");
			const getJSON = await getShibe.json();

			if(getJSON[0])
			this.selectedItem = getJSON[0];
			alert(getJSON);
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
