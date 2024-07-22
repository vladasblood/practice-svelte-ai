<script lang="ts">
	import Bounded from '$lib/components/Bounded.svelte';
	import type { Content } from '@prismicio/client';
	import { PrismicImage, PrismicRichText } from '@prismicio/svelte';
	import GoldText from './GoldText.svelte';
	import Heading2 from '$lib/components/Heading2.svelte';

	export let slice: Content.BentoSlice;
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<PrismicRichText
		field={slice.primary.heading}
		components={{ em: GoldText, heading2: Heading2 }}
	/>
	<PrismicRichText field={slice.primary.body} />

	{#each slice.primary.repeatable_zone as item}
		<!-- Render content for item -->
		<PrismicRichText field={item.title} />
		<PrismicRichText field={item.body} />
		<PrismicImage field={item.image} />
	{/each}
</Bounded>
