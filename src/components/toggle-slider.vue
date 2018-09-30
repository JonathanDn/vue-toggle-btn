<template>
	<!--Binding css variables to use as height/width of :before -> the slider -->
	<div class="toggle-slider"
	     :style="{  '--handle-diameter' : options.handle.diameter + 'px',
					'--handle-color': options.handle.color,
					'--handle-border-radius': options.handle.borderRadius,
					'--track-width': options.track.width + 'px',
					'--track-height': options.track.height + 'px',
					'--track-color': options.track.color,
					'--track-active-color': options.track.activeColor,
					'--track-border-width': options.track.borderWidth + 'px',
					'--track-border-radius': options.track.borderRadius,
					'--handle-distance': getHandleDistance + 'px'}">
		<label class="switch">
			<input type="checkbox">
			<span class="track">
				<span class="handle"></span>
			</span>
		</label>
	</div>
</template>

<script>
	export default {
		name: 'toggleButton',
		props: ["options"],
		data() {
			return {

			}
		},
		computed: {
			getHandleDistance: function() {
				return this.options.track.width - this.options.handle.diameter;
			}
		},
		methods: {

		},
		beforeCreate() {

		}
	}
</script>

<style scoped lang="scss">
	.switch {
		position: relative;
		display: inline-block;
		width: var(--track-width);
		height: var(--track-height);
		input {
			display: none;
		}
		.track {
			display: flex;
			align-items: center;
			position: absolute;
			width: 100%;
			height: 100%;
			top: 0;
			left: 0;
			right: 0;
			bottom: 0;
			background-color: var(--track-color);
			cursor: pointer;
			border: var(--track-border-width) solid var(--track-color);
			border-radius: var(--track-border-radius);
			transition: .4s;
			.handle {
				display: flex;
				width: var(--handle-diameter);
				height: var(--handle-diameter);
				background-color: var(--handle-color);
				border-radius: var(--handle-border-radius);
				transition: .4s;
			}
		}
		input:checked + .track {
			background-color: var(--track-active-color);
			border: var(--track-border-width) solid var(--track-active-color);
		}
		input:focus + .track {
			box-shadow: 0 0 1px var(--track-active-color);
		}
		input:checked + .track > .handle {
			transform: translateX(var(--handle-distance));
		}
	}
</style>
