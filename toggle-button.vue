<template>
	<!--Binding css variables to use as height/width of :before -> the slider -->
	<div class="toggle-slider"
	     :style="{
	                '--handle-diameter' : handle.diameter + 'px',
					'--handle-color': handle.color,
					'--handle-border-radius': handle.borderRadius,
					'--handle-distance': getHandleDistance + 'px',

					'--track-color': track.color,
					'--track-width': track.width + 'px',
					'--track-height': track.height + 'px',
					'--track-active-color': track.activeColor,
					'--track-border-width': track.borderWidth + 'px',
					'--track-border-radius': track.borderRadius
				}">
		<label class="switch">
			<input v-model="isActive" type="checkbox" @click="setNewToggleState">
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
				handle: {
					diameter: 30, // optional
					distance: 40, // optional
					color: '#fff', // optional
					borderRadius: "50%", // optional
				},
				track: {
					color: '#ccc', // optional
					width: 70, // optional
					height: 30, // optional
					activeColor: '#2196F3', // optional
					borderWidth: 0, // optional
					borderRadius: '34px', // optional
				},
				isActive: false,
			}
		},
		computed: {
			getHandleDistance: function() {
				let handleDistance = 0;
				if (this.options && this.options.handle && this.options.track) {
					handleDistance = this.options.track.width - this.options.handle.diameter;
				} else {
					handleDistance = this.handle.distance;
				}
				return handleDistance;
			}
		},
		methods: {
			setConfigData() {
				if (this.options) {
					if (this.options.handle) {
						this.setBindedProp(this.handle, this.options.handle, 'diameter');
						this.setBindedProp(this.handle, this.options.handle, 'color');
						this.setBindedProp(this.handle, this.options.handle, 'borderRadius');
					}
					if (this.options.track) {
						// TODO - track border width, track border radius - 24.12.18
						this.setBindedProp(this.track, this.options.track, 'color');
						this.setBindedProp(this.track, this.options.track, 'width');
						this.setBindedProp(this.track, this.options.track, 'height');
						this.setBindedProp(this.track, this.options.track, 'activeColor');
						this.setBindedProp(this.track, this.options.track, 'borderWidth');
						this.setBindedProp(this.track, this.options.track, 'borderRadius');
					}
					if (this.options.isActive) {
						this.isActive = this.options.isActive;
					}
				}
			},
			setBindedProp(localProp, propParent, propToBind) {
				if (propParent[propToBind]) {
					localProp[propToBind] = propParent[propToBind];
				}
			},
			setNewToggleState() {
				this.isActive = !this.isActive;
				this.$emit('setIsActive', this.isActive);
			}
		},
		beforeCreate() {

		},
		created() {
			this.setConfigData();
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
