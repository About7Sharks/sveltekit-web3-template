<script>
	import { browser } from '$app/env';
	import { onMount } from 'svelte';
	import Web3Modal from 'web3modal';
	import { defaultEvmStores, selectedAccount, connected } from 'svelte-web3';
	let web3Modal, provider;
	// ------------------------------------------------------------- //

	const onConnect = async () => {
		await clearCache();
		try {
			provider = await web3Modal.connect();
			await defaultEvmStores.setProvider(provider);
		} catch (e) {
			console.log('Could not get a wallet connection', e);
			return;
		}
		// Subscribe to events here if needed (e.g. "accountsChanged")
		provider.on('accountsChanged', (accounts) => {
			console.log('accounts changed: ' + accounts);
		});
	};
	const onDisconnect = async () => {
		await clearCache();
	};
	const clearCache = async () => {
		await defaultEvmStores.disconnect();
		await web3Modal.clearCachedProvider();
	};
	// ------------------------------------------------------------- //

	onMount(async () => {
		if (browser) {
			const WalletConnectProvider = window.WalletConnectProvider.default;
			const providerOptions = {
				walletconnect: {
					package: WalletConnectProvider,
					options: {
						rpc: {
							56: 'https://bsc-dataseed.binance.org/'
						},
						network: 'binance'
					}
				}
			};
			web3Modal = new Web3Modal({ providerOptions });
		}
	});
</script>

{#if $connected}
	<button on:click={onDisconnect} class="outline btn-info"> Disconnect </button>
{:else}
	<button on:click={onConnect} class="outline btn-info"> Connect </button>
{/if}

<style scoped>
	button {
		width: 100%;
		/* position: relative;
		top: 5px;
		right: 5px; */
		/* background-color: rgb(30, 66, 131);
		color: white;
		border-radius: 25px;
		border: 1px solid white;
		font-size: 18px;
		cursor: pointer; */
	}
</style>
