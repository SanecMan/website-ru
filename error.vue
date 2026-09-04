<template>
	<div class="h-full text-center flex flex-col items-center justify-center">
		<div class="p-8">
			<h1 v-if="error.statusCode === 404">Страница не найдена</h1>
			<h1 v-else>Произошла ошибка</h1>
			<NuxtLink to="/">На главную</NuxtLink>
		</div>
	</div>
</template>

<script setup>
const props = defineProps({
	error: {
		type: Object,
		default: null,
	},
})

const title = computed(() => {
	if (props.error.statusCode === 404) {
		return 'Страница не найдена'
	}
	return 'Произошла ошибка'
})

useHead({
	title: `${title.value} - Space Station 13`,
})
</script>
