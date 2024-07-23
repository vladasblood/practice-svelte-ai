<script>
	import { PrismicLink } from '@prismicio/svelte';
	import WordMark from './WordMark.svelte';
	import ButtonLink from './ButtonLink.svelte';
	import clsx from 'clsx';

	import IconClose from '~icons/ph/x-bold';
	import IconMenu from '~icons/ph/list-bold';

	/** @type {import("@prismicio/client").Content.SettingsDocument}*/

	export let settings;

	let isOpen = true;
	const toggleOpen = () => (isOpen = !isOpen);
	const close = () => (isOpen = false);
</script>

<header class="p-4 md:p-6">
	<nav
		class="flex-max-w-6xl font mx-auto flex-col justify-between py-2 font-medium text-white md:flex-row md:items-center"
		aria-label="Main"
	>
		<div class="flex items-center justify-between">
			<a href="/">
				<WordMark />
				<span class="sr-only">{settings.data.site_title} home page</span>
			</a>

			<button type="button" class="block p-2 text-3xl text-white md:hidden" on:click={toggleOpen}
				><IconMenu /></button
			>
		</div>

		<!-- Mobile Nav -->
		<div
			class={clsx(
				'tranistion-transform fixed inset-0 z-40 flex flex-col items-end bg-gray-950 pr-4 pt-14 duration-300 ease-in-out md:hidden',
				isOpen ? 'translate-x-0' : 'translate-x-[100%]'
			)}
		>
			<button type="button" class="block p-2 text-3xl text-white md:hidden" on:click={toggleOpen}
				><IconClose /></button
			>

			<ul class="grid justify-items-end gap-8">
				{#each settings.data.navigation as item (item.label)}
					<li>
						{#if item.cta_button}
							<ButtonLink field={item.link}>
								{item.label}
							</ButtonLink>
						{:else}
							<PrismicLink field={item.link} class="block min-h-11 px-3 text-3xl first:mt-8">
								{item.label}
							</PrismicLink>
						{/if}
					</li>
				{/each}
			</ul>
		</div>

		<!-- Desktop Nav -->
		<ul class="flex gap-6">
			{#each settings.data.navigation as item (item.label)}
				<li>
					{#if item.cta_button}
						<ButtonLink field={item.link}>
							{item.label}
						</ButtonLink>
					{:else}
						<PrismicLink field={item.link} class="inline-flex min-h-11 items-center">
							{item.label}
						</PrismicLink>
					{/if}
				</li>
			{/each}
		</ul>
	</nav>
</header>
