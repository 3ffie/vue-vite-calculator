<template>
	<Calculator2/>
	<MillimeterToKilometer/>
</template>

<script>
import Calculator2 from '../components/Calculator2.vue';
import MillimeterToKilometer from '../components/MillimeterToKilometer.vue';

	export default {
		components: {
			Calculator2,
			MillimeterToKilometer,
		}
	}
</script>

<style>
	* {
		box-sizing: border-box;
		padding: 0;
		margin: 0;
	}

	body {
		background: rgb(115, 75, 145);
		color: white;
	}
</style>