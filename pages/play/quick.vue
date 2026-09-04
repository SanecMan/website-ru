<template>
	<div class="container mx-auto px-4">
		<div class="flex">
			<div
				class="flex items-center bg-secondary px-4 py-2 rounded-t-sm ml-auto md:mr-4 text-sm"
			>
				<Icon name="fa6-regular:circle-question" class="mr-2" />
				<div>
					Это небольшой список серверов, отобранных для новичков. Полный список
					всех серверов —
					<NuxtLink to="/play/browser">здесь</NuxtLink>.
				</div>
			</div>
		</div>
		<div class="card server-blurbs">
			<div v-if="!servers?.length" class="p-10 text-center">
				<Icon name="svg-spinners:6-dots-scale" size="2em" />
			</div>
			<template v-else>
				<ServerBlurb
					v-for="(server, index) in servers"
					:key="index"
					v-bind="server"
				/>
			</template>
		</div>
	</div>
</template>

<script setup>
definePageMeta({
	name: 'PageQuickPlay',
	title: 'Быстрый старт',
})

const { data: servers } = await useAsyncData(
	'servers',
	() => {
		return queryCollection('servers').order('created', 'asc').all()
	},
	{ server: false },
)
</script>

<style lang="scss" scoped>
.server-blurbs {
	> *:not(:last-child) {
		@apply mb-10;
	}
}
</style>
