<script lang="ts">
	import clsx from 'clsx';
	import Bounded from '$lib/components/Bounded.svelte';
	import type { Content } from '@prismicio/client';
	import { PrismicImage, PrismicRichText, PrismicText } from '@prismicio/svelte';
	import GoldText from './GoldText.svelte';
	import Heading2 from '$lib/components/Heading2.svelte';

	export let slice: Content.BentoSlice;
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<PrismicRichText
		field={slice.primary.heading}
		components={{ em: GoldText, heading2: Heading2 }}
	/>

	<div class="mx-auto mt-6 max-w-md text-balance text-center text-gray-300">
		<PrismicRichText field={slice.primary.body} />
	</div>

	<div class="grid-row-[auto_auto_auto] mt-16 grid max-w-4xl gap-8 md:grid-cols-3 md:gap-10">
		{#each slice.primary.repeatable_zone as item}
			<!-- Render content for item -->
			<div
				class={clsx(
					'glass-container row-span-3 grid grid-rows-subgrid gap-4 rounded-lg bg-gray-950/60 p-4 before:bg-gray-100/10',
					item.wide ? 'md:col-span-2' : 'md-col-span-1'
				)}
			>
				<h3 class="text-2xl">
					<PrismicText field={item.title} />
				</h3>
				<div class="max-w-md text-balance text-gray-300">
					<PrismicRichText field={item.body} />
				</div>
				<PrismicImage field={item.image} class="max-h-36 w-auto" />
			</div>
		{/each}
	</div>
</Bounded>
