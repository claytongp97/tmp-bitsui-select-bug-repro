<script lang="ts">
	import { Select } from 'bits-ui';
	import CaretDoubleDown from 'phosphor-svelte/lib/CaretDoubleDown';
	import CaretDoubleUp from 'phosphor-svelte/lib/CaretDoubleUp';
	import CaretUpDown from 'phosphor-svelte/lib/CaretUpDown';
	import Check from 'phosphor-svelte/lib/Check';

	let value = $state<string>('');
</script>

<Select.Root type="single" onValueChange={(v) => (value = v)}>
	<Select.Trigger class=" flex rounded-sm border p-2" aria-label="Select a theme">
		Selection: {value === '' ? 'None' : value}
		<CaretUpDown class="ml-4 size-6 text-muted-foreground" />
	</Select.Trigger>
	<Select.Portal>
		<Select.Content
			class="focus-override z-50 h-96 max-h-[var(--bits-select-content-available-height)] w-[var(--bits-select-anchor-width)]"
		>
			<Select.ScrollUpButton class="flex w-full items-center justify-center">
				<CaretDoubleUp class="size-3" />
			</Select.ScrollUpButton>
			<Select.Viewport class="p-1">
				{#each { length: 100 } as _, i (i)}
					{@const item = { value: `item-${i}`, label: `Item ${i + 1}` }}
					<Select.Item
						class="rounded-button flex h-10 w-full items-center py-3 pr-1.5 pl-5 text-sm capitalize outline-hidden select-none data-disabled:opacity-50 data-highlighted:bg-muted"
						value={item.value}
						label={item.label}
					>
						{#snippet children({ selected })}
							{item.label}
							{#if selected}
								<div class="ml-auto">
									<Check aria-label="check" />
								</div>
							{/if}
						{/snippet}
					</Select.Item>
				{/each}
			</Select.Viewport>
			<Select.ScrollDownButton class="flex w-full items-center justify-center">
				<CaretDoubleDown class="size-3" />
			</Select.ScrollDownButton>
		</Select.Content>
	</Select.Portal>
</Select.Root>
