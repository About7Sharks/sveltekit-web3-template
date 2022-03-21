<script>
	import ConnectButton from '$lib/ConnectButton.svelte';
	import { selectedAccount, connected, chainId } from 'svelte-web3';

	let account, chain;
	$: account = $connected ? $selectedAccount : '---';
	$: chain = $connected ? $chainId : '---';
</script>

<svelte:head>
	<title>SvelteKit Web3 Demo</title>
</svelte:head>

<div>
	<h1>SvelteKit Web3 Demo App</h1>

	<ConnectButton />
	<!-- if connected -->
	{#if $connected}
		<p>ChainId: {chain} | Account: {account}</p>
	{:else}
		<p>Connect Bich</p>
	{/if}
</div>
