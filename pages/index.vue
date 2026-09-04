<template>
	<div>
		<HeroHeader />

		<main class="content py-12 lg:text-lg lg:py-16 xl:py-24 debris-bg">
			<div class="max-w-screen-xl mx-auto px-4">
				<div class="card mb-8 lg:mb-12">
					<h2 class="mb-4 lg:mb-5 content-heading content-heading--primary">
						Выживи, если сможешь
					</h2>

					<p class="mb-4 lg:mb-6">
						В недалёком будущем члены экипажа на космических станциях
						корпораций без устали поддерживают жизнь на борту. Одной работы
						недостаточно — им приходится бороться за выживание в суровых
						условиях космоса и противостоять опасностям, что скрываются во
						тьме.
					</p>
					<p>
						Создайте свою историю в мире Space Station 13 — многопользовательской
						песочнице с огромным количеством возможностей. Более 22 лет разработки
						и тысячи авторов делают мир SS13 постоянно живым и меняющимся.
					</p>
				</div>

				<TestimonialSlider class="mt-4 mb-6 lg:mt-8 lg:mb-10 lg:mx-10" />

				<div class="flex flex-col lg:flex-row lg:mb-8">
					<div class="flex flex-col mb-8 lg:mr-8 lg:mb-0">
						<h2 class="mb-4 lg:mb-8 content-heading content-heading--primary">
							Геймплей и возможности
						</h2>

						<ul
							class="flex h-full flex-col justify-between gap-4 ml-6 features"
						>
							<li>
								Играйте за самые разные роли на станции: от простого ассистента
								до инженера, держащего станцию под напряжением, и капитана,
								управляющего всем железной рукой.
							</li>
							<li>
								Нарушайте порядок как антагонист: ядерные оперативники с РПГ,
								оборотни-ксеносы, мстительные волшебники и многое другое.
							</li>
							<li>
								Проявляйте креативность в сложных системах — от детальной
								медицинской симуляции до исследований таинственных артефактов с
								опасными, но полезными эффектами.
							</li>
							<li>
								Наслаждайтесь полностью управляемым игроками геймплеем: ни один
								раунд не повторит другой.
							</li>
							<li>
								Открывайте древние руины и странных существ на соседних
								планетах — и раскрывайте их тайны.
							</li>
							<li>
								Вычисляйте самозванцев среди экипажа, которые охотятся на вас и
								других! Разоблачайте их умом или криминалистикой.
							</li>
							<li>
								Столкнитесь со случайными опасностями: разгерметизацией,
								радиационными бурями, сбойным ИИ и метеоритными дождями.
							</li>
						</ul>
					</div>

					<div
						class="flex gap-6 justify-center flex-wrap lg:justify-start lg:flex-col lg:gap-8 lg:flex-shrink-0 lg:w-4/12"
					>
						<BaseImage
							class="game-shot-card"
							src="/img/about-preview-1.jpg"
							width="1000"
							height="710"
							:img-attrs="{ loading: 'lazy', alt: 'Превью' }"
						/>
						<BaseImage
							class="game-shot-card"
							src="/img/about-preview-2.jpg"
							width="1000"
							height="714"
							:img-attrs="{ loading: 'lazy', alt: 'Превью' }"
						/>
					</div>
				</div>
			</div>
		</main>
	</div>
</template>

<script setup>
definePageMeta({
	name: 'IndexPage',
	layout: 'home',
})
</script>

<style lang="scss" scoped>
.features {
	li {
		position: relative;

		&:before {
			content: '';
			position: absolute;
			top: 10px;
			left: -16px;
			width: 8px;
			height: 8px;
			background: theme('colors.primary');
		}
	}
}
</style>
