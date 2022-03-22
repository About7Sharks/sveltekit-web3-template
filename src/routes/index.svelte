<script>
	import ConnectButton from '$lib/ConnectButton.svelte';
	import Header from '$lib/Header.svelte';
	import { selectedAccount, connected, chainId } from 'svelte-web3';

	let account, chain;
	$: account = $connected ? $selectedAccount : '---';
	$: chain = $connected ? $chainId : '---';
</script>

<svelte:head>
	<title>SvelteKit Web3 Demo</title>
</svelte:head>

<div>
	<!-- <h1>SvelteKit Web3 Demo App</h1> -->
	<Header />
	<!-- if connected -->
	{#if $connected}
		<!-- <p>ChainId: {chain} | Account: {account}</p> -->
	{:else}
		<!-- <ConnectButton /> -->
	{/if}
	<div class="hero fullscreen">
		<div class="hero-body u-center">
			<div class="w-90" style="position: relative">
				<div class="row">
					<div class="col-6" style="padding: 2rem;">
						<div class="u-flex u-items-center">
							<h1>Hoopakele 🍍</h1>
							<b class="p-2"
								>Now in <div class="tag tag--link">BETA</div></b
							>
						</div>

						<p class="lead">
							Aloha, welcome to your web3 dashboard. Sign in below to start exploring endless the
							new possibilities of the web.
						</p>

						<div class="form-group">
							<!-- <input type="text" placeholder="Enter your email address." /> -->
							<ConnectButton />
						</div>
					</div>

					<div class="col-6" style="padding: 2rem;">
						<img
							src="https://cdn.dribbble.com/users/509287/screenshots/6453164/attachments/1380683/1600x1200__1_.png"
						/>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
