<template>
	<v-app>
			<v-row>
				<v-col
					cols="12"
					class="orange"
				>
					<TagList
						:tags="tags"
						:align="'left'"
						:fontSize="16"
						:iconSize="18"
						class="ma-4"
					/>
				</v-col>

				<v-col
					cols="12"
					class="red"
				>
					<TagList
						:tags="tags"
						:align="'justify'"
						:fontSize="18"
						:iconSize="20"
						class="ma-4"
					/>
				</v-col>

				<v-col
					cols="6"
					class="light-blue"
				>
					<TagList
						:tags="tags"
						:align="'left'"
						:fontSize="14"
						:iconSize="16"
						class="ma-4"
					/>
				</v-col>

				<v-col
					cols="6"
					class="light-green"
				>
					<TagList
						:tags="tags"
						:align="'justify'"
						:fontSize="12"
						:iconSize="14"
						class="ma-4"
					/>
				</v-col>
			</v-row>
	</v-app>
</template>

<script>
	import TagList from "./components/TagList.vue";

	export default {
		name: "App",
		components: {
			TagList
		},
		data() {
			return {
				tags: [
					{
						text: "текст1"
					},
					{
						text: "текст2",
						icon: "mdi-star"
					},
					{
						text: "текст3"
					},
					{
						text: "текст4",
						icon: "mdi-heart"
					},
					{
						text: "текст5"
					}
				]
			}
		}
	}
</script>