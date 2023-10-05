<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
</script>

<AppShell>
	<svelte:fragment slot="header">
		<AppBar>
			<svelte:fragment slot="lead">Tic Tac Toe</svelte:fragment>
			<svelte:fragment slot="trail">🙂🙂🙂</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<slot />
</AppShell>
