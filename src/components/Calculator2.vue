<template>
	<main class="calculator-main">
		<div class="display">
			{{showingResult ? currentResult : currentInput}}
		</div>

		<div class="input">
			<div class="calculator-numbers">
				<button @click="clearResult" class="calculator-button calculator-clear">C</button>
				<button @click="handleNumberInput(number)" class="calculator-button calculator-button_number" v-for="number in 9">{{ number }}</button>
				<button @click="handleNumberInput('.')" class="calculator-button">.</button>
				<button @click="handleNumberInput(0)" class="calculator-button calculator-button_number calculator-button_number__zero">0</button>
			</div>
				<!--operators-->
				<!-- the +/- button almost works. It will calculate a negative value, but it will not display a "-" -->
				<!--added a % operator but i doesn't work-->
			<div class="calculator-operators">
				<button @click="handleOperatorInput('+/-')" class="calculator-button calculator-button__operator">+/-</button>
				<button @click="handleOperatorInput('/')" class="calculator-button calculator-button__operator">/</button>
				<button @click="handleOperatorInput('*')" class="calculator-button calculator-button__operator">*</button>
				<button @click="handleOperatorInput('-')" class="calculator-button calculator-button__operator">-</button>
				<button @click="handleOperatorInput('+')" class="calculator-button calculator-button__operator">+</button>
				<button @click="handleOperatorInput('%')" class="calculator-button calculator-button__operator">%</button>
				<button @click="handleEqualsInput" class="calculator-button calculator-button__equal">=</button>
			</div>
		</div>
	</main>
</template>

<script>
	export default {
		data() {
			return {
				showingResult: false,
				currentResult: 0,
				currentInput: '',
				currentOperator: null,
			}
		},

		created() {
			window.addEventListener('keyup', this.handleKeyup);
		},

		computed: {
			currentInputAsNumber() {
				return Number(this.currentInput)
			},
		},

		methods: {
			calculateResult() {
				switch (this.currentOperator) {
					case '+':
						this.currentResult += this.currentInputAsNumber;
						break;
					case '-':
						this.currentResult -= this.currentInputAsNumber;
						break;
					case '/':
						this.currentResult /= this.currentInputAsNumber;
						break;
					case '*':
						this.currentResult *= this.currentInputAsNumber;
						break;
					case '+/-':
						this.currentResult *= this.currentInputAsNumber -1;
						break;
					case '%':
						this.currentResult = (this.currentInputAsNumber)/100; 
					default:
						this.currentResult = this.currentInputAsNumber;
				}
			},

			clearResult() {
				this.currentResult = 0;
				this.currentInput = '';
				this.currentOperator = null;
				this.showingResult = false;
			},

			handleNumberInput(number) {
				this.currentInput += number;
				this.showingResult = false;
			},

			handleOperatorInput(operator) {
				this.calculateResult();
				this.currentOperator = operator;
				this.currentInput = '';
				this.showingResult = true;
			},

			handleEqualsInput() {
				this.calculateResult();
				this.showingResult = true;
			},

			handleKeyup(event) {
				switch(event.key) {
					case '0':
					case '1':
					case '2':
					case '3':
					case '4':
					case '5':
					case '6':
					case '7':
					case '8':
					case '9':
						this.handleNumberInput(event.key)
						break;
					case '+':
					case '/':
					case '-':
					case '*':
						this.handleOperatorInput(event.key)
						break;
					case '.':
					case ',':
						this.handleNumberInput('.')
						break;
					case '=':
					case 'Enter':
						this.handleEqualsInput()
						break;
					case 'Escape':
					case 'Backspace':
						this.clearResult()
						break;
				}
			}
		}
	}
		
</script>

<style>
	body {
		display: flex;
		justify-content: center;
		align-items: center;
		margin: 20px 20px;
	}
	.calculator-main {
		position: relative;
		margin: 15px;
		padding: 5px;
		display: flex;
		flex-flow: column nowrap;
		

		width: 20rem;
		height: 30rem;
		font-family:Verdana, Geneva, Tahoma, sans-serif;
		border: 0.5px solid rgb(83, 62, 78);
		border-radius: 10px;
		overflow: hidden;
		
		background: rgb(186, 149, 178);
		color: white;

	}

	.display {
		font-size: 20px;
		padding: 0.5rem;
		width: 100%;
		height: 5rem;
		border: 2px solid rgb(200, 114, 181);
		border-radius: 5px;
		overflow: hidden;
		text-overflow: ellipsis;
		text-align: end;
	}

	.input {
		display: flex;
		gap: 2px;
		height: 100%;
		
	}

	.calculator-numbers {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		width: 80%;
		gap: 2px;
	}

	.calculator-operators {
		display: flex;
		height: 100%;
		width: 20%;
		flex-flow: column nowrap;
		column-gap: 2px;
		row-gap: 2px;
	}

	.calculator-button {
		font-size: medium;
		width: 100%;
		height: 100%;
		border: 2px solid rgb(200, 114, 181);
		border-radius: 3px;
		padding: 0.5rem;
		background-color: rgb(204, 128, 187);	
		color: white;
	}

	.calculator-button__operator {
		background: rgb(197, 116, 209)
	}

	.calculator-button:hover {
		background:rgb(197, 116, 209)
	}

	.calculator-button__operator:hover {
		background: rgb(204, 128, 187)
	}

	.calculator-button__equal {
		background: rgb(226, 123, 163);
	}
	.calculator-clear {
		grid-column: span 3;
	}

</style>