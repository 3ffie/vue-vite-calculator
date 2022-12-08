<template>
	<section class="converter">
		<input class="converter-input converter-input__mm" type="number" placeholder="MM" v-model="valueMillimeters"/>
		<div class="converter-output">{{ valueCentimeter }} cm</div>
		<div class="converter-output">{{ valueMeter }} m</div>
		<div class="converter-output">{{ valueKilometer }} km</div>
		<div class="converter-output">{{ valueMetricMileNorway }} mile</div>
	</section>
</template>


<script>
	export default {
		data() {
			return {
				valueMillimeters: 10,
				valueCentimeters: 10,
			}
		},
		
		computed: {
			valueCentimeter() {
				return (this.valueMillimeters / 10)	 
			},

			valueMeter() {
				return (this.valueMillimeters / 1000)
			},

			valueKilometer() {
				return (this.valueMillimeters / 10000)
			},

			valueMetricMileNorway() {
				return (this.valueMillimeters / 100000 )
			},

		}
	}
</script>

<style>
	.converter {
		display: grid;
		justify-content: center;
		align-items: center;
	}

	.converter-input {
		background: rgb(200, 114, 181);
		color: white;
		border-radius: 7px;
		border: 2px solid rgb(213, 183, 206);
		border-style: dotted;
		padding: 5px;
		margin: 5px 5px;
	}

	.converter-output {
		display: flex;
		justify-content: space-between;
		border-radius: 7px;
		border: 2px solid rgb(213, 183, 206);
		padding: 5px;
		margin: 7px 5px;
	}

	::placeholder {
		color: white;
		opacity: 50;
	}
</style>
