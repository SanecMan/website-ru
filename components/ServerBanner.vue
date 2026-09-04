<template>
	<div class="server-banner">
		<div>
			<div class="text-sm uppercase font-medium tracking-wide">
				{{ title }}
			</div>
			<div class="text-xs italic">
				<span v-if="loading" class="flex items-center opacity-50">
					<Icon name="svg-spinners:6-dots-scale" class="mr-1" />
					Обновление...
				</span>
				<span v-else-if="error" class="text-primary">
					Ошибка статуса
				</span>
				<span v-else class="opacity-50">
					{{ players }}
					{{ playersWord }} онлайн
				</span>
			</div>
		</div>
		<a
			:href="joinLink"
			target="_blank"
			rel="external"
			class="cta cta--sm ml-2 py-1"
		>
			Войти
		</a>
	</div>
</template>

<script setup>
const props = defineProps({
	title: {
		type: String,
		required: true,
	},
	ip: {
		type: String,
		required: true,
	},
	port: {
		type: Number,
		required: true,
	},
	url: {
		type: String,
		required: false,
		default: '',
	},
})

const loading = ref(true)
const error = ref(false)
const players = ref(null)

const joinLink = computed(() => {
	if (props.url) return props.url
	return `byond://${props.ip}:${props.port}`
})

const playersWord = computed(() => {
	const n = players.value
	const mod10 = n % 10
	const mod100 = n % 100
	if (mod10 === 1 && mod100 !== 11) return 'игрок'
	if (mod10 >= 2 && mod10 <= 4 && (mod100 < 12 || mod100 > 14)) return 'игрока'
	return 'игроков'
})

const fetchData = async () => {
	loading.value = true
	try {
		const data = await useNodeApi('/status', {
			params: {
				ip: props.ip,
				port: props.port,
			},
		})

		let gameData = data.meta.jsontopic ? data.response.data : data.response
		if (typeof gameData === 'string') gameData = JSON.parse(gameData)
		if (!('players' in gameData) || Number.isNaN(gameData.players)) {
			throw new TypeError('No players key')
		}
		players.value = parseInt(gameData.players)
		error.value = false
	} catch {
		error.value = true
	}
	loading.value = false
}

onMounted(() => {
	fetchData()
})
</script>

<style lang="scss" scoped>
.server-banner {
	@apply flex items-center justify-between border-l-2 border-primary
					bg-background bg-opacity-50 text-white rounded-sm
					pl-4 pr-2 py-2;
}
</style>
