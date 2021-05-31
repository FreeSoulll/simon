<template>
  <button  :class="classes" @click="handleClick" ref="button" />
</template>

<script>

import {reactive } from 'vue'

	export default {
		emits:['click'],
		props: {
			idx: {
				type: Number,
				required: true,
			},
			color: {
				type: String,
				required: true,
			},
			name: {
				type: String,
				required: true,
			},
		},

		setup(props,context) {
			const classes = reactive(['simon-button',props.color])
			const path = require(`../assets/sounds/${props.name}`)
			const sounds = reactive({
				sound: new Audio(path),
			})

			function	play() {
				sounds.sound.play();
				classes.push('active')
				setTimeout(() => {
					classes.splice(-1)
				}, 400)
			}

			function	handleClick() {
				play()
				context.emit('click', props.idx)
			}

			return {
				sounds,
				classes,
				play,
				handleClick
			}
		},
	};
</script>

<style scoped>
	.simon-button {
		width: inherit;
		height: inherit;
		border: none;
		/* transition: background-color 0.1s ease-out; */
	}

	.simon-button:focus {
		box-shadow: inset 0px 0px 50px 0 rgba(0, 0, 0, 0.25);
		outline: none;
	}

	.simon-button.blue {
		background-color: var(--blue-color);
	}

	.simon-button.blue.active {
		background-color: var(--blue-color-active);
	}

	.simon-button.blue:hover {
		background-color: var(--blue-color-hover);
	}

	.simon-button.red {
		background-color: var(--red-color);
	}

	.simon-button.red.active {
		background-color: var(--red-color-active);
	}

	.simon-button.red:hover {
		background-color: var(--red-color-hover);
	}

	.simon-button.yellow {
		background-color: var(--yellow-color);
	}

	.simon-button.yellow.active {
		background-color: var(--yellow-color-active);
	}

	.simon-button.yellow:hover {
		background-color: var(--yellow-color-hover);
	}

	.simon-button.green {
		background-color: var(--green-color);
	}

	.simon-button.green.active {
		background-color: var(--green-color-active);
	}

	.simon-button.green:hover {
		background-color: var(--green-color-hover);
	}
</style>
