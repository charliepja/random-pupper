<template lang="html">
	<img :src="pic">
</template>

<script>
export default {
	name: "got-image",
	props: ['pic']
}
</script>

<style lang="css" scoped>
	img {
		width: 450px;
		height: 450px;
		border: 3px solid black;
	}
</style>
