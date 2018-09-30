<template>
	<div id="app">
		<toggle-slider :options="options"></toggle-slider>
	</div>
</template>

<script>
	import ToggleSlider from './components/toggle-slider.vue'

	export default {
		name: 'app',
		data() {
			return {
				options: {
					handle: {
						diameter: 30,
						color: "#fff",
						borderRadius: "50%"
					},
					track: {
						width: 70,
						height: 30,
						color: "#ccc",
						activeColor: "#2196F3",
						borderWidth: 2,
						borderRadius: "34px"
					}
				}
			}
		},
		components: {
			ToggleSlider
		}
	}
</script>

<style>
	#app {

	}
</style>