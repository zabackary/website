<script lang="ts">
	import Button from "components/Button.svelte";

	interface Props {
		title: string;
		description: string;
		author: string;
		date: Date;
		url: string;
		thumbnail?: string | undefined;
		thumbnailAlt?: string | undefined;
		style?: string;
	}

	let {
		title,
		description,
		author,
		date,
		url,
		thumbnail = undefined,
		thumbnailAlt = undefined,
		style = "",
	}: Props = $props();
</script>

<div class="blog-card" {style}>
	{#if thumbnail}
		<img class="blog-card-thumbnail" src={thumbnail} alt={thumbnailAlt} />
	{/if}
	<a class="blog-card-title" href={url}>
		<span>{title}</span>
	</a>
	<p class="blog-card-description">{description}</p>
	<div class="blog-card-metadata">
		<a
			class="blog-card-author"
			href={`https://github.com/${author}`}
			target="_blank"
			rel="noreferrer noopeners"
		>
			<img src={`https://github.com/${author}.png`} alt="Author Profile" />
			<span>
				<strong>{author}</strong> • {date.toLocaleDateString("en-US", { timeZone: 'UTC' })}
			</span>
		</a>
		<Button class="blog-card-button" variant="accent" href={url}>
			Read More
		</Button>
	</div>
</div>

<style>
	.blog-card {
		position: relative;
		overflow: hidden;
		display: flex;
		flex-direction: column;
		flex: 0 0 auto;
		padding: 24px;
		border-radius: 8px;
		background: var(--background-secondary);
		box-shadow:
			2.8px 2.8px 2.2px rgba(0, 0, 0, 0.02),
			6.7px 6.7px 5.3px rgba(0, 0, 0, 0.028),
			12.5px 12.5px 10px rgba(0, 0, 0, 0.035),
			22.3px 22.3px 17.9px rgba(0, 0, 0, 0.042),
			41.8px 41.8px 33.4px rgba(0, 0, 0, 0.05),
			100px 100px 80px rgba(0, 0, 0, 0.07);
		animation: slide-up 500ms backwards 650ms;
		z-index: 1;
	}

	.blog-card-thumbnail {
		user-select: none;
		object-fit: cover;
		inset: 0;
		z-index: -1;
		position: absolute;
		inline-size: 100%;
		block-size: 100%;
		mask: radial-gradient(
			circle at top left,
			rgba(0, 0, 0, 0.025),
			rgba(0, 0, 0, 0.15)
		);
	}

	.blog-card-title {
		text-decoration: none;
		margin: 0;
		line-height: 1.5;
		margin-block-end: 8px;
		font-weight: 400;
		font-size: 1.8rem;
		font-family: var(--font-monospace);
		color: var(--foreground-primary);
	}

	.blog-card-title span {
		border-bottom: 1px solid transparent;
	}

	.blog-card-title:hover span {
		border-color: currentColor;
	}

	.blog-card-description {
		margin: 0;
		color: var(--foreground-secondary);
		font-size: 1.4rem;
	}

	.blog-card-metadata {
		margin-block-start: 16px;
		display: flex;
		flex-wrap: wrap;
		gap: 24px;
		justify-content: space-between;
		align-items: flex-end;
	}

	.blog-card-author {
		text-decoration: none;
		display: flex;
		align-items: center;
		font-size: 1.4rem;
		color: var(--foreground-secondary);
	}

	.blog-card-author strong {
		border-bottom: 1px solid transparent;
		font-weight: 600;
		color: var(--foreground-primary);
	}

	.blog-card-author:hover strong {
		border-color: currentColor;
	}

	.blog-card-author img {
		border-radius: 50%;
		margin-inline-end: 8px;
		inline-size: 24px;
		block-size: auto;
	}

	.blog-card :global(.blog-card-button) {
		padding-block: 8px;
		white-space: nowrap;
	}
</style>
