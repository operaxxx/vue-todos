<template>
		<li>
			<Checkbox v-model="isChecked"></Checkbox>
			{{todo.content}}
			<a href="#" style="margin-left:20px" @click="$emit('remove')">
				<Icon type="md-close" />
			</a>
		</li>
</template>

<script>
export default {
	props : {
		todo : {
		},
		index : {

		}
	},
	data() {
		return {
			isChecked : false
		}
	},
};
</script>

<style scoped>
	li {
		padding-bottom: 4px;
		color:dimgray;
		font-size: 18px;
	}
</style>
