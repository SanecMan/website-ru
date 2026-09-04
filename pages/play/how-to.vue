<template>
	<div class="container mx-auto px-4">
		<div class="flex items-center gap-8 lg:gap-14 mb-8">
			<BaseImage
				class="hidden md:block game-shot-card max-w-[420px]"
				src="/img/how-to-preview.jpg"
				width="1000"
				height="711"
				:img-attrs="{ alt: 'Превью' }"
			/>

			<div class="flex-grow-1">
				<h2 class="mb-4 lg:mb-8 font-semibold uppercase tracking-wide text-3xl">
					Добро пожаловать в Space Station 13
				</h2>
				<p class="text-xl leading-8">
					Начать просто, быстро и — главное — совершенно бесплатно! Следуйте
					шагам ниже, и уже через пару минут вы будете в игре.
				</p>
			</div>
		</div>

		<div class="card">
			<div class="flex gap-4 sm:gap-8">
				<div class="how-to-step"><span>1</span></div>
				<div class="flex-grow pb-6 md:pb-10 pt-2">
					<h3 class="content-heading content-heading--secondary mb-4">
						Скачать
					</h3>
					<p class="mb-4">
						Space Station 13 работает на платформе BYOND (Build Your Own Net
						Dream) — её нужно скачать и установить, чтобы играть.
					</p>
					<a href="https://www.byond.com/download/" class="cta" target="_blank">
						Скачать BYOND
						<Icon
							name="fa6-solid:square-arrow-up-right"
							class="relative ml-2 bottom-[-2px]"
						/>
					</a>
				</div>
			</div>

			<div class="flex gap-4 sm:gap-8">
				<div class="how-to-step"><span>2</span></div>
				<div class="flex-grow pb-6 md:pb-10 pt-2">
					<h3 class="content-heading content-heading--secondary mb-4">
						Регистрация
					</h3>
					<p class="mb-4">
						Затем создайте аккаунт BYOND. При запуске вас попросят войти — все
						серверы Space Station 13 требуют аккаунт.
					</p>
					<a href="https://secure.byond.com/Join" class="cta" target="_blank">
						Создать аккаунт
						<Icon
							name="fa6-solid:square-arrow-up-right"
							class="relative ml-2 bottom-[-2px]"
						/>
					</a>
				</div>
			</div>

			<div class="flex gap-4 sm:gap-8">
				<div class="how-to-step how-to-step--no-line"><span>3</span></div>
				<div class="flex-grow pt-2">
					<h3 class="content-heading content-heading--secondary mb-4">Играть!</h3>
					<p class="mb-4">
						В мире Space Station 13 множество серверов — у каждого своё
						сообщество и стиль игры. Это может пугать, поэтому мы собрали
						короткий список популярных серверов, либо вы можете сразу открыть
						полный список и выбрать то, что зацепит взгляд.
					</p>
					<div class="flex flex-col md:flex-row flex-wrap gap-4 md:gap-6 py-4">
						<NuxtLink to="/play/quick" class="list-link card">
							<strong>Быстрый старт</strong>
							<p>
								Подборка популярных серверов, удобная для новичков.
							</p>
						</NuxtLink>
						<NuxtLink to="/play/interesting" class="list-link card">
							<strong>Интересные сервера</strong>
							<p>
								Отдельная подборка серверов, которые стоит посмотреть.
							</p>
						</NuxtLink>
						<NuxtLink to="/play/browser" class="list-link card">
							<strong>Полный список серверов</strong>
							<p>
								Подробный список всех серверов онлайн прямо сейчас — для тех,
								кто любит исследовать.
							</p>
						</NuxtLink>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
definePageMeta({
	name: 'PageHowToPlay',
	title: 'Как начать',
})
</script>

<style lang="scss" scoped>
.how-to-step {
	@apply relative flex-shrink-0;

	&:before {
		content: '';
		position: absolute;
		left: 50%;
		top: 0;
		bottom: 0;
		width: 7px;
		margin-left: -3px;
		background: #565c6c;
	}

	&--no-line:before {
		content: none;
	}

	> span {
		@apply relative rounded-full text-3xl font-medium w-16 h-16 justify-center flex items-center;
		// background: rgba(lighten($color-secondary, 25%), 0.6);
		background: #565c6c;

		@screen sm {
			@apply w-20 h-20 text-4xl;
		}
	}
}

.list-link {
	@apply relative flex flex-col text-white shadow-inner;
	background: #454a56;

	@screen md {
		@apply flex-1 min-w-[220px];
	}

	&:before {
		@apply transition-all duration-300 rounded-b-sm bg-opacity-90;
		content: '';
		position: absolute;
		bottom: -1px;
		left: -1px;
		right: -1px;
		height: 4px;
		background: linear-gradient(
			135deg,
			var(--color-primary) 0%,
			rgb(177 48 40) 100%
		);
	}

	> * {
		@apply relative z-10;
	}

	strong {
		@apply mb-2 uppercase tracking-wide;
	}

	&:hover,
	&:active {
		&:before {
			@apply rounded-t-sm;
			height: calc(100% + 2px);
		}
	}
}
</style>
