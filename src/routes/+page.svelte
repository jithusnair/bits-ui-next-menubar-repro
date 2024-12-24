<script lang="ts">
	import { Menubar } from 'bits-ui';

	let openState = $state(false);
	let input = $state<HTMLInputElement>();

	function onOpenChange(value: boolean) {
		openState = value;
	}

	function handleFocus(e: Event) {
		e.preventDefault();
		input?.focus();
	}
</script>

<h1 class="mt-4 text-center text-4xl">Menubar Issue</h1>

<Menubar.Root
	{onOpenChange}
	class="rounded-10px border-dark-10 bg-background-alt shadow-mini flex h-12 items-center gap-1 border px-[3px]"
>
	<Menubar.Menu>
		<Menubar.Trigger
			class="rounded-9px data-[highlighted]:bg-muted data-[state=open]:bg-muted inline-flex h-10 cursor-default items-center justify-center px-3 text-sm font-medium !ring-0 !ring-transparent"
		>
			HELP ME
		</Menubar.Trigger>
		<Menubar.Portal>
			<Menubar.Content
				onCloseAutoFocus={handleFocus}
				class="focus-override border-muted bg-background shadow-popover z-50 w-fit rounded-xl border px-1 py-1.5 focus-visible:outline-none"
			>
				<Menubar.Item
					class="rounded-button data-[highlighted]:bg-muted flex h-10 min-w-[130px] select-none items-center py-3 pl-3 pr-1.5 text-sm font-medium !ring-0 !ring-transparent"
				>
					Hello
				</Menubar.Item>
			</Menubar.Content>
		</Menubar.Portal>
	</Menubar.Menu>
</Menubar.Root>

<section>
	<h3><code>onOpenChange</code> not fired.</h3>
	<p><code>openState</code> should update when <code>onOpenChange</code> is called.</p>
	<p>
		<code>openState:</code>
		{openState}.
	</p>
</section>

<section>
	<h3><code>onCloseAutoFocus</code> not fired?</h3>
	<label for="test-input">Input should focus after closing menu.</label>
	<input bind:this={input} id="test-input" class="border px-2" type="text" placeholder="Focus" />

	<button class="rounded bg-blue-700 px-1 py-1 text-white" onclick={handleFocus}
		>Click to focus</button
	>
	<button class="rounded bg-red-700 px-1 py-1 text-white" onclick={() => input?.blur()}
		>Click to blur</button
	>
</section>

<section>
	<h3>Typescript clues?</h3>
	<p>Also finding squiggly lines for <code>onOpenChange</code> prop. Not sure if that helps.</p>
	<img src="/squiggly-lines.png" alt="" />
</section>

<style lang="pcss">
	section {
		@apply mx-4 mt-8;
	}

	h3 {
		@apply mb-2 text-lg font-bold;
	}
</style>
