<script lang="ts">
	import { onMount } from 'svelte';

	import { discordUrl } from '../data';

	import CsIdea from '$lib/CsIdea.svelte';
	import Card from '$lib/Card.svelte';
	import Footer from '$lib/Footer.svelte';
	import BorderlessCard from '$lib/BorderlessCard.svelte';

	const scrollerText1 = `Our mission is to bring <span class="accent">valuable experience</span> to upcoming developers.`;
	const scrollerText2 = `We focus on<br />real-world <span class="accent">app development</span> instead of CS concepts.`;

	/**
	 * Variables for the scroller animation
	 */
	let nav: HTMLElement;
	let header: HTMLElement;
	let headerImage: HTMLImageElement;

	/* Scrolling animation */
	const progressPadding = 0.05;

	let scroller: HTMLElement;
	let canvas: HTMLDivElement;
	let phone: HTMLImageElement;

	let progress: number;
	let canvasWidth: number;
	let phoneWidth: number;

	let windowHeight: number;

	function scrollEvent() {
		// Calculate progress from 0.0 to 1.0 based on scroll position in scroller
		//   window.scrollY - scroller.offsetTop = scroll position in the scroller element
		//   (...) / offsetHeight                = progress from 0.0 to 1.0
		//   (...) * 2                           = shift progress endpoint backwards one viewport
		if (scroller) progress = ((window.scrollY - scroller.offsetTop) / scroller.offsetHeight) * 2;

		// Clamp progress to 0 and 1
		progress = Math.max(0, progress);
		progress = Math.min(1, progress);

		// Set values from 0.0 -> padding to 0.0
		if (progress <= progressPadding) progress = 0;
		// Set values from (1.0 - padding) -> 1.0 to 1.0
		else if (progress >= 1 - progressPadding) progress = 1;
		// Stretch values in between to match new endpoints
		else progress = (1 - progressPadding * 2) * (progress - progressPadding);

		// TODO: temporary until fix found
		resizeEvent();
	}

	function resizeEvent() {
		header.style.height = window.innerHeight - nav.offsetHeight + 'px';

		canvasWidth = canvas ? canvas.offsetWidth : 0;
		phoneWidth = phone ? phone.width : 0;

		windowHeight = window.innerHeight;
	}

	let javascriptEnabled = false;
	onMount(() => {
		/* Detect JavaScript */
		javascriptEnabled = true;

		/* Remove maxHeight when JavaScript is enabled */
		headerImage.style.maxHeight = 'initial';

		/* Update on window resize */
		addEventListener('resize', resizeEvent);

		/* Scrolling animation */
		addEventListener('scroll', scrollEvent);

		// Fire once when page is loaded to initialize states
		resizeEvent();
		scrollEvent();
	});
</script>

<nav bind:this={nav}>
	<CsIdea />
	<div class="nav-links">
		<!-- <a href="/">Home</a> -->
		<!-- <a href="#projects">Projects</a> -->
		<!-- <a href="/members">Members</a> -->
		<!-- <a href="/outreach">Outreach</a> -->
		<a class="nav-highlight" href={discordUrl}>Join</a>
	</div>
</nav>

<header bind:this={header}>
	<div class="header-body">
		<h1>Go beyond<br /><span class="accent">CompSci.</span></h1>
		<p>
			The <strong>CRHS Innovation and Development Association</strong> (IDEA) helps students go beyond
			school curriculum and step into the world of software development.
		</p>
		<div class="header-socials">
			<!-- <a href="https://github.com/crhsidea"><img src="/assets/github.svg" /></a> -->
			<!-- <a href="https://discord.gg/d66XHcxWEH"><img src="/assets/discord.svg" /></a> -->
			<a href={discordUrl}>Discord</a>
			<a href="https://github.com/crhsidea">Github</a>
		</div>
	</div>
	<img
		bind:this={headerImage}
		class="header-image"
		src="/assets/texture.svg"
		alt="Patterned image"
		aria-hidden="true"
	/>
</header>

<main>
	{#if javascriptEnabled && windowHeight >= 550}
		<section bind:this={scroller} class="scroller">
			<div>
				<div bind:this={canvas}>
					{#if progress <= 0.5}
						<p style={'opacity: ' + (1 - progress * 2)}>{@html scrollerText1}</p>
						<div
							class="phone-container"
							style={'transform: translateX(-' +
								Math.abs(canvasWidth - phoneWidth) * progress * 2 +
								'px)'}
						>
							<img
								bind:this={phone}
								src="/assets/phone.svg"
								style={'max-height: 25rem; transform: rotateZ(' + (15 - progress * 45) + 'deg)'}
								alt="Phone screen"
							/>
						</div>
					{:else}
						<div class="phone-container">
							<img
								bind:this={phone}
								src="/assets/phone.svg"
								alt="Phone screen"
								style={'max-height: 25rem; transform: rotateZ(-7.5deg)'}
							/>
						</div>
						<p style={'text-align: right; opacity: ' + (progress - 0.5) * 2}>
							{@html scrollerText2}
						</p>
					{/if}
				</div>
			</div>
		</section>
	{:else}
		<section class="nojs-scroller">
			<div class="phone-container">
				<img
					bind:this={phone}
					src="/assets/phone.svg"
					alt="Phone screen"
					style={'max-height: 70vh; transform: rotateZ(-7.5deg)'}
				/>
			</div>
			<div>
				<p>{@html scrollerText1}</p>
				<br />
				<p>{@html scrollerText2}</p>
			</div>
		</section>
	{/if}

	<section class="cards">
		<div class="cards-container">
			<div class="cards-top">
				<!-- <Card title="30+ hackathons"> -->
				<Card title="15+ hackathons">
					We attend in-person and virtual hackathons where we apply our skills and challenge
					ourselves to create something innovative.
				</Card>

				<!-- <Card title="20+ wins"> -->
				<Card title="7+ wins">
					Through our collaborative efforts and teamwork, we've managed to win a handful of times.
					The prizes vary across hackathons, but they usually include money.
				</Card>
			</div>
			<Card title="200+ volunteer hours">
				We offer volunteering hours for tutoring computer science to other students. By
				volunteering, you may be eligible for the Presidential Volunteer Service Award.
			</Card>
		</div>
	</section>

	<section class="hackathons section-center">
		<h2>Hackathons</h2>
		<p>
			We attend in-person and virtual hackathons where we apply our skills and challenge ourselves
			to create something innovative.
		</p>

		<img src="/assets/hackathon0.jpg" alt="Picture of TAMUHack 2023" />
	</section>

	<section class="section-center">
		<h2>Tutoring</h2>
		<p>
			We offer opportunities for those who can tutor computer science curriculum, and for those who
			need help with the material.
		</p>
		<div class="tutoring-container">
			<BorderlessCard title="Java" iconUrl="/assets/java.svg">
				Java is taught in higher level CS classes to introduce more advanced topics.
			</BorderlessCard>
			<BorderlessCard title="Python" iconUrl="/assets/python.svg">
				Python is commonly taught to people just being introduced to programming.
			</BorderlessCard>
			<BorderlessCard title="Dart" iconUrl="/assets/dart.svg">
				Dart is the language of the Flutter framework, which we use for hackathons.
			</BorderlessCard>
		</div>
	</section>

	<!-- <section id="projects" class="section-center"> -->
	<!-- 	<h2>Past projects</h2> -->
	<!-- 	<p> -->
	<!-- 		Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut -->
	<!-- 		labore et dolore magna aliqua. -->
	<!-- 	</p> -->
	<!-- </section> -->

	<section class="section-center">
		<h2>Help! What if...</h2>

		<div class="faq-details">
			<details>
				<summary>I missed the join deadline</summary>
				What deadline? There is no deadline. You can join any time want, and we'll catch you up.
			</details>

			<details>
				<summary>I don't know what a hackathon is</summary>
				A hackathon is a programming event where teams of four people or less work to create an app in
				a time constraint. These can range from 48 hours to a week. The main goal of hackathons are the
				viability and execution of an idea. Think of this as a startup competition. Also free food!
			</details>

			<details>
				<summary>I don't know how to code, but I want to attend a hackathon</summary>
				Hackathons are generally very beginner-friendly. While hackathons are competitions, it's more
				important to learn and have fun. There typically are plenty of side-events for you to participate
				in.
			</details>
		</div>
	</section>
</main>

<Footer />

<style lang="scss">
	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: var(--spacing--page-x);

		margin-left: var(--spacing--page-x);
		margin-bottom: var(--spacing-xl);

		overflow-x: hidden;

		p {
			color: var(--color-text--body);
		}

		strong {
			color: var(--color-text);
		}

		.header-image {
			height: 100%;

			// Disabled when JavaScript is enabled
			max-height: 85vh;
		}
	}

	@media (width < 760px) {
		.header-body {
			margin-right: var(--spacing--page-x);
		}

		.header-image {
			display: none;
		}
	}

	@media (width < 512px) {
		:root {
			--font-xl: 4rem;
			--font--scroller: 3rem;
			--spacing--page-x: 1rem;
		}
	}

	.header-body {
		height: fit-content;

		h1 {
			margin-bottom: 1rem;
		}

		.header-socials {
			display: flex;
			gap: 0.5rem;

			margin-top: 2rem;

			a {
				padding: 0.5rem 1.5rem;
				border-radius: 999px;
				color: var(--color-text--accent-contrast);
				background-color: var(--color-background--card);

				transition: filter 0.15s;

				&:hover {
					filter: brightness(0.8);
				}
			}
		}
	}

	section:not(:first-child) {
		margin-top: var(--spacing-md);
	}

	.section-center {
		display: flex;
		flex-direction: column;
		align-items: center;

		text-align: center;

		& > h2 {
			margin-bottom: var(--spacing-md);
		}

		& > p {
			max-width: 40ch;

			margin-bottom: var(--spacing-md);

			color: var(--color-text--body);
		}
	}

	.scroller {
		display: block;
		height: 250vh;

		.accent {
			font-weight: bold;
		}

		& > div {
			position: sticky;
			top: 0;
			display: flex;
			justify-content: center;
			align-items: center;

			height: 100dvh;
			height: 100vh;

			& > div {
				display: flex;
				justify-content: center;
				align-items: center;
			}

			p {
				font-size: var(--font--scroller);
				max-width: 12ch;
				line-height: 110%;
			}
		}
	}

	@media (width < 850px) {
		.phone-container {
			display: none !important;
		}

		.scroller p {
			text-align: left !important;
		}
	}

	.nojs-scroller {
		display: flex;
		justify-content: center;
		gap: var(--spacing-xl);

		.accent {
			font-weight: bold;
		}

		img {
			position: sticky;
			top: var(--spacing-xl);
		}

		div {
			display: flex;
			flex-direction: column;
			gap: var(--spacing-lg);
		}

		p {
			/* font-size: var(--font-xl); */
			font-size: var(--font--scroller);
			max-width: 12ch;
			line-height: 110%;
		}
	}

	.cards {
		display: flex;
		justify-content: center;
	}

	.cards-container {
		width: var(--size--max-width);
	}

	.cards-top {
		display: flex;
		gap: var(--spacing-md);

		margin-bottom: var(--spacing-md);

		// flex: 1;
	}

	@media (width < 800px) {
		.cards-top {
			flex-direction: column;
		}
	}

	.hackathons {
		img {
			width: 75%;
			border-radius: 1rem;
		}
	}

	@media (width < 850px) {
		.hackathons img {
			width: var(--size--max-width);
		}
	}

	.tutoring-container {
		display: flex;
		flex-wrap: wrap;
		gap: var(--spacing-lg);

		margin-top: var(--spacing-lg);
	}

	.faq-details {
		display: flex;
		flex-direction: column;
		gap: var(--spacing-md);

		width: min(40rem, 100%);

		details {
			width: 100%;
			padding: var(--spacing-sm);
			border-radius: var(--border-sm);

			background-color: var(--color-background--card);

			text-align: initial;

			summary {
				display: flex;

				color: var(--color-text--accent-contrast);

				&::marker {
					content: '';
				}

				&::before {
					content: url(/assets/chevron.svg);

					display: inline-flex;

					transition: transform 0.15s;
					will-change: transform;
				}
			}

			&[open] summary {
				margin-bottom: var(--spacing-sm);
				&::before {
					transform: rotate(180deg);
				}
			}
		}
	}

	@media (prefers-color-scheme: dark) {
		details {
			color: var(--color-text--body);
		}

		summary::before {
			content: url(/assets/chevron-dark.svg) !important;
		}
	}
</style>
