<script lang="ts">
	import type {NFTValue} from '../utils/nft';

	export let etherscanURL: string | undefined = undefined;
	export let tokenID: string | bigint;
	export let tokenAddress: `0x${string}`;

	export let account: `0x${string}`;
	$: tokenIDAsString = typeof tokenID === 'bigint' ? tokenID.toString() : BigInt(tokenID).toString();

	export let value: NFTValue;
</script>

<li>
	<div class=body style=--elevation:1>

	{#if value.visuals}
		{#if value.visuals[0].type === 'image'}
			<img src={value.visuals[0].url} alt={value.name || 'unnamed NFT'} />
			{#if etherscanURL}<a
					class="overlay"
					href={`${etherscanURL}/nft/${tokenAddress}/${tokenIDAsString}`}
					target="_blank"
					rel="noreferrer"
					><span>{value.name|| 'unnamed NFT'}</span>
				</a>
				<a href={`${etherscanURL}/address/${account}`} class=account target="_blank" rel="noreferrer"><span class=dis>account:&nbsp;</span> {account}</a>
				
			{:else}
				<div class="overlay"><span>{value.name || 'unnamed NFT'}</span></div>
			{/if}
		{:else if value.visuals[0].type === 'iframe'}
			<div style="height: 350px;">
				<span
					>Iframe not implemented yet {#if etherscanURL}<a
							style="text-decoration: underline; color: blue;"
							href={`${etherscanURL}/nft/${tokenAddress}/${tokenIDAsString}`}
							target="_blank"
							rel="noreferrer">See on Etherscan</a
						>
					{/if}</span
				>
			</div>
		{/if}
	{:else}
		<div style="height: 350px;">
			<span
				>No Image {#if etherscanURL}<a
						style="text-decoration: underline; color: blue;"
						href={`${etherscanURL}/nft/${tokenAddress}/${tokenIDAsString}`}
						target="_blank"
						rel="noreferrer">See on Etherscan</a
					>
				{/if}</span
			>
		</div>
	{/if}
	</div>
</li>

<style>




	li img {
		object-fit: cover;
		max-width: 100%;
		height: auto;
		vertical-align: middle;
		border-radius: 5px;
	}
	.overlay {
		position: absolute;
		width: 100%;
		height: auto;
		background: rgba(57, 57, 57, 0.502);
		top: 0;
		left: 0;
		transform: scale(0);
		transition: all 0.01s 0.1s ease-in-out;
		color: #fff;
		border-radius: 5px;
		/* center overlay text */
		display: flex;
		align-items: top;
		justify-content: center;
	}
	.dis {
		color:  #6875ED;

	}
	.account {
		font-size: x-small;
		width: 100%;
		height: 16px;
		box-shadow: 0px 0.883215px 2.64964px rgba(0, 0, 0, 0.2);
    outline-width: 1px;
    outline-color: #E88B88;

		color: #E88B88;
		border-radius: 1px;
		/* center overlay text */
		display: flex;
		align-items: top;
		justify-content: center;
	}

	/* hover */
	li:hover .overlay {
		transform: scale(1);
	}

	li {
		/* fallback */
		display: inline-block;
		width: 350px;
		margin: 0 5px 10px 5px;
		/* end fallback */
		position: relative;
		cursor: pointer;
	}
	li {
		flex-basis: 350px; /*width: 350px;*/
		margin: 0;
	}
</style>
