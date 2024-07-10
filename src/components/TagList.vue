<template>
	<div
		ref="tagListContainer"
		class="tag-list"
	>
		<div
			:class="[
				'tag-list__container d-flex flex-nowrap',
				{ 'justify-space-between': align === 'justify' }
			]"
		>
			<div
				v-for="(tag, index) in visibleTags"
				:key="index"
				:class="[
					'tag-list__tag-wrapper d-flex align-center',
					{ 'flex-fill d-flex align-center': align === 'justify' && index < visibleTags.length - 1 }
				]"
			>
				<v-chip
					class="tag-list__tag"
					color="white"
					:style="{ fontSize: fontSize + 'px' }"
					text-color="dark"
				>
					<v-icon
						v-if="tag.icon"
						:size="iconSize"
						class="tag-list__icon mr-1"
					>
						{{ tag.icon }}
					</v-icon>

					{{ tag.text }}
				</v-chip>

				<v-icon
					v-if="index < visibleTags.length - 1"
					class="tag-list__separator mx-auto"
					color="white"
					:size="iconSize"
				>
					mdi-circle-small
				</v-icon>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		name: "TagList",
		props: {
			tags: {
				type: Array,
				required: true
			},
			align: {
				type: String,
				default: "left"
			},
			fontSize: {
				type: Number,
				default: 14
			},
			iconSize: {
				type: Number,
				default: 16
			}
		},
		data() {
			return {
				visibleTags: [],
			};
		},
		mounted() {
			this.updateVisibleTags();
			window.addEventListener("resize", this.updateVisibleTags);
		},
		beforeDestroy() {
			window.removeEventListener("resize", this.updateVisibleTags);
		},
		methods: {
			updateVisibleTags() {
				this.$nextTick(() => {
					const containerWidth = this.$refs.tagListContainer.getBoundingClientRect().width;
					let currentWidth = 0;
					this.visibleTags = [];
					const separatorWidth = this.iconSize;
					const gapWidth = 16;

					for (const [index, tag] of this.tags.entries()) {
						const tagElement = document.createElement("div");
						tagElement.style.visibility = "hidden";
						tagElement.style.position = "absolute";
						tagElement.style.fontSize = this.fontSize + 'px';
						tagElement.innerHTML = tag.icon ? `<v-icon style="font-size: ${this.iconSize}px;">${tag.icon}</v-icon> ${tag.text}` : tag.text;
						document.body.appendChild(tagElement);
						const tagWidth = tagElement.offsetWidth;
						document.body.removeChild(tagElement);

						if (currentWidth + tagWidth + (index > 0 ? gapWidth : 0) > containerWidth) {
							break;
						}

						currentWidth += tagWidth + (index > 0 ? gapWidth : 0);
						if (index < this.tags.length - 1) {
							currentWidth += separatorWidth;
						}

						this.visibleTags.push(tag);
					}
				})
			}
		},
		watch: {
			tags: {
				handler() {
					this.updateVisibleTags();
				},
				immediate: true
			}
		}
	}
</script>