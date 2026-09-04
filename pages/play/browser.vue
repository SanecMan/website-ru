<template>
	<div class="container mx-auto px-4">
		<div class="card p-0 hub-servers">
			<div class="hub-filters">
				<Pagination
					:total-pages="totalPages"
					:per-page="perPage"
					:current-page="page"
					@pagechanged="onPageChange"
				/>
				<div class="flex items-center gap-2">
					<span
						v-if="searchedServers.length"
						class="hidden sm:inline flex-shrink-0 text-sm italic opacity-60"
					>
						Показано {{ searchedServers.length }}
						{{ serversWord }}
					</span>
					<HubServerSearch v-model="search" />
					<HubFilters :filters="filters" @filters-changed="onFiltersChange" />
				</div>
			</div>
			<div v-if="loading" class="p-10 text-center">
				<Icon name="svg-spinners:6-dots-scale" size="2em" />
			</div>
			<div v-else-if="error" class="p-10 text-center text-primary">
				<Icon name="fa6-solid:circle-exclamation" size="2em" class="mb-2" />
				<div class="font-medium">
					Не удалось загрузить серверы. Обновите страницу и попробуйте снова.
				</div>
			</div>
			<template v-else>
				<template v-if="filteredServers.length">
					<HubServer
						v-for="server in filteredServers"
						:key="server.id"
						v-bind="server"
					/>
				</template>
				<div v-else class="p-10 text-center italic">Серверы не найдены.</div>
			</template>
			<div class="hub-filters">
				<Pagination
					:total-pages="totalPages"
					:per-page="perPage"
					:current-page="page"
					@pagechanged="onPageChange"
				/>
				<div class="flex items-center gap-2">
					<HubServerSearch v-model="search" />
					<HubFilters :filters="filters" @filters-changed="onFiltersChange" />
				</div>
			</div>
		</div>

		<div class="disclaimer">
			<Icon name="fa6-solid:circle-exclamation" size="8em" />
			<p class="mb-2 font-bold">Внимание!</p>
			<p>
				Некоторые серверы по умолчанию скрыты: они помечены как 18+ и могут
				содержать контент, не подходящий для всех. Чтобы показать их в списке,
				нажмите на значок настроек рядом с поиском. Часть серверов скрыта
				постоянно по решению администрации сайта.
			</p>
		</div>
	</div>
</template>

<script setup>
definePageMeta({
	name: 'PageServerBrowser',
	title: 'Список серверов',
})

const loading = ref(true)
const error = ref(false)
const servers = ref([])
const search = ref('')
const page = ref(1)
const perPage = ref(15)
const filters = ref({})

const searchedServers = computed(() => {
	return servers.value.filter((server) => {
		if (server?.meta?.adult && !filters.value.includeAdult) return false
		return server.status.toLowerCase().includes(search.value.toLowerCase())
	})
})

const filteredServers = computed(() => {
	return searchedServers.value.slice(
		perPage.value * (page.value - 1),
		perPage.value * page.value,
	)
})

const totalPages = computed(() => {
	return Math.floor(searchedServers.value.length / perPage.value) || 1
})

const serversWord = computed(() => {
	const n = searchedServers.value.length
	const mod10 = n % 10
	const mod100 = n % 100
	if (mod10 === 1 && mod100 !== 11) return 'сервер'
	if (mod10 >= 2 && mod10 <= 4 && (mod100 < 12 || mod100 > 14)) return 'сервера'
	return 'серверов'
})

watch(totalPages, (val) => {
	if (val < page.value) page.value = val
})

onMounted(async () => {
	loading.value = true
	try {
		const { response } = await useNodeApi('/hub', { timeout: 5000 })
		const serverList = response.sort((a, b) => b.players - a.players)
		servers.value = serverList
	} catch {
		error.value = true
	}
	loading.value = false
})

const onPageChange = (newPage) => {
	page.value = newPage
}

const onFiltersChange = (newFilters) => {
	filters.value = newFilters
}
</script>

<style lang="scss" scoped>
.hub-filters {
	@apply flex flex-col gap-2 justify-between bg-background bg-opacity-50 p-4;

	.pagination {
		@apply w-full;
	}

	@screen sm {
		@apply flex-row gap-4;

		.pagination {
			@apply w-auto;
		}
	}
}

.disclaimer {
	@apply relative bg-secondary bg-opacity-50 rounded-sm pl-12 pr-4 py-6 mt-12
		overflow-hidden;

	> span {
		@apply absolute -top-6 -left-11 opacity-25;
		z-index: -1;
	}
}
</style>
