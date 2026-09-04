<template>
	<div class="slider text-center h-32 sm:h-24 md:h-20">
		<transition-group
			tag="div"
			class="h-full relative overflow-hidden"
			:name="transitionName"
		>
			<div
				v-if="show"
				:key="current"
				class="slide absolute inset-0 flex flex-col justify-center"
			>
				<div class="slide-inner">
					<p class="font-serif sm:text-lg lg:text-xl">
						&#8220;{{ slides[current].quote }}&#8221;
					</p>
					<p class="font-semibold uppercase tracking-wider opacity-75">
						{{ slides[current].author }}
					</p>
				</div>
			</div>
		</transition-group>
	</div>
</template>

<script setup>
const current = ref(0)
const direction = ref(1)
const transitionName = ref('fade')
const show = ref(false)
const loop = ref(0)
const slides = ref([
	{
		quote:
			'Space Station 13 — одна из лучших песочниц-симуляторов, бесплатных или нет.',
		author: 'Rock, Paper, Shotgun',
	},
	{
		quote:
			'Возможно почти всё, каждый раунд уникален, и все немного безумны. И это лишь часть причин, почему я люблю Space Station 13.',
		author: 'PC GAMER',
	},
	{
		quote:
			'Станцию захватили культисты... Что мне делать? Беру швабру и вытираю кровавую лужу. Потому что это моя работа. Я просто уборщик.',
		author: 'PCGamesN',
	},
	{
		quote:
			'Необходимость массового сотрудничества незнакомцев из интернета создаёт уморительный хаос. Готовьтесь взрываться. Часто.',
		author: 'PC GAMER UK',
	},
	{
		quote:
			'Научно-фантастическая многопользовательская песочница с тем же безумным подходом «чем больше, тем лучше», что и у Dwarf Fortress.',
		author: 'Rock, Paper, Shotgun',
	},
	{
		quote:
			'Space Station 13 не похожа ни на одну другую игру, потому что, как и многое великое, она получилась случайно.',
		author: 'https://return.life - Robert Mariani',
	},
])

const slide = (dir) => {
	direction.value = dir
	transitionName.value = dir === 1 ? 'slide-next' : 'slide-prev'
	const len = slides.value.length
	current.value = (current.value + (dir % len) + len) % len
}

onMounted(() => {
	show.value = true
	loop.value = setInterval(() => {
		slide(1)
	}, 10000)
})

onBeforeUnmount(() => {
	clearInterval(loop.value)
})
</script>

<style lang="scss" scoped>
/* FADE IN */
.fade-enter-active {
	transition: opacity 1s;
}
.fade-enter-from {
	opacity: 0;
}

/* GO TO NEXT SLIDE */
.slide-next-enter-active,
.slide-next-leave-active {
	transition: transform 0.5s ease-in-out;
}
.slide-next-enter-from {
	transform: translate(100%);
}
.slide-next-leave-to {
	transform: translate(-100%);
}

/* GO TO PREVIOUS SLIDE */
.slide-prev-enter-active,
.slide-prev-leave-active {
	transition: transform 0.5s ease-in-out;
}
.slide-prev-enter-from {
	transform: translate(-100%);
}
.slide-prev-leave-to {
	transform: translate(100%);
}
</style>
