<script lang="ts">
	import { onMount } from 'svelte';

	// --- State ---
	let showAnnouncement = true;
	let prefersReducedMotion = false;

	// --- Content (from JSON) ---
	// In a real app, this would be loaded from a static JSON file or an API.
	const content = {
		title: 'Silo Automation: Reclaim Your Time',
		metaDescription:
			'Automate repetitive tasks, integrate your tools, and unlock peak efficiency. Start for free and see results in minutes.',
		ogImageUrl: 'https://example.com/og-image.png',
		canonicalUrl: 'https://example.com/',
		organization: {
			name: 'Silo Automation, Inc.',
			logo: 'https://example.com/logo.png',
			url: 'https://example.com/'
		},
		product: {
			name: 'Silo Automator',
			description: 'The ultimate platform for streamlining your digital workflows.'
		},
		announcement: {
			text: 'New Integration: Connect with XYZ Platform in one click!',
			cta: 'Learn More'
		},
		hero: {
			hook: 'Stop Wasting Time on Repetitive Tasks.',
			subHook: 'Our platform automates your workflows so you can focus on what truly matters.',
			primaryCta: 'Get Started for Free',
			secondaryCta: 'Watch a Demo',
			trustCues: ['No credit card required', '14-day free trial', 'Cancel anytime']
		},
		socialProof: {
			logos: [
				{ name: 'InnovateCorp', src: '/logos/innovatecorp.svg' },
				{ name: 'QuantumLeap', src: '/logos/quantumleap.svg' },
				{ name: 'Synergy Inc.', src: '/logos/synergy.svg' },
				{ name: 'Apex Solutions', src: '/logos/apex.svg' },
				{ name: 'Momentum Co.', src: '/logos/momentum.svg' }
			],
			counts: 'Trusted by 10,000+ teams worldwide'
		},
		valueProps: [
			{ title: 'Integrate Everything', description: 'Connect all your tools in a single, unified hub.' },
			{ title: 'Automate Workflows', description: 'Build powerful automations with a simple drag-and-drop interface.' },
			{ title: 'Gain Full Visibility', description: 'Track every process with real-time analytics and dashboards.' },
			{ title: 'Scale with Confidence', description: 'Our enterprise-grade platform grows with your business needs.' }
		],
		features: [
			{
				title: 'Visual Workflow Builder',
				description: 'Design complex automations without writing a single line of code.',
				image: '/screenshots/feature-builder.png'
			},
			{
				title: 'One-Click Integrations',
				description: 'Connect to hundreds of popular apps from our extensive library.',
				image: '/screenshots/feature-integrations.png'
			},
			{
				title: 'Advanced Analytics',
				description: 'Get deep insights into your operational efficiency and identify bottlenecks.',
				image: '/screenshots/feature-analytics.png'
			}
		],
		howItWorks: [
			{
				step: 1,
				title: 'Connect Your Apps',
				description: 'Authorize your favorite tools with our secure, one-click process.'
			},
			{
				step: 2,
				title: 'Build Your Silo',
				description: 'Visually map out your process using our intuitive drag-and-drop editor.'
			},
			{
				step: 3,
				title: 'Activate & Monitor',
				description: 'Go live and watch your automated workflows deliver results in real-time.'
			}
		],
		personas: [
			{
				persona: 'For Marketing Teams',
				problem: 'Struggling to sync lead data between your CRM and email platform?',
				outcome: 'Automate lead nurturing and track campaign ROI from a single dashboard.'
			},
			{
				persona: 'For Operations',
				problem: 'Manual data entry and report generation slowing you down?',
				outcome: 'Eliminate errors and get real-time reports delivered to your inbox automatically.'
			},
			{
				persona: 'For Developers',
				problem: 'Spending too much time on internal tool scripts and API glue code?',
				outcome: 'Offload maintenance to us and trigger workflows via our robust developer API.'
			}
		],
		metrics: [
			{ value: '50%', label: 'Reduction in manual data entry', proof: 'According to a case study with Acme Corp.' },
			{ value: '8h', label: 'Average time saved per employee per week', proof: 'Based on internal customer surveys.' },
			{ value: '3x', label: 'Faster project delivery cycles', proof: 'Observed in teams after 30 days of use.' }
		],
		integrations: {
			text: 'Works with the tools you already love.',
			logos: [
				{ name: 'Tool A', src: '/logos/tool-a.svg' },
				{ name: 'Tool B', src: '/logos/tool-b.svg' },
				{ name: 'Tool C', src: '/logos/tool-c.svg' },
				{ name: 'Tool D', src: '/logos/tool-d.svg' },
				{ name: 'Tool E', src: '/logos/tool-e.svg' },
				{ name: 'Tool F', src: '/logos/tool-f.svg' }
			]
		},
		testimonials: [
			{
				quote: "This platform transformed our operations. We're saving hundreds of hours a month.",
				name: 'Jane Doe',
				title: 'COO, InnovateCorp'
			},
			{
				quote: 'The flexibility of the workflow builder is unmatched. If you can think it, you can automate it.',
				name: 'John Smith',
				title: 'Head of Marketing, QuantumLeap'
			},
			{
				quote: 'A game-changer for our dev team. We retired a mountain of legacy scripts in the first week.',
				name: 'Emily White',
				title: 'Lead Engineer, Synergy Inc.'
			}
		],
		pricing: {
			teaser: 'Simple, transparent pricing',
			plan: 'Starts from $49/mo',
			cta: 'View All Plans'
		},
		faq: [
			{ q: 'Is there a free trial?', a: 'Yes! All new users get a 14-day free trial of our Pro plan, no credit card required.' },
			{ q: 'What happens after my trial ends?', a: 'You can choose to upgrade to a paid plan or be automatically downgraded to our Free plan, which has limited features.' },
			{ q: 'Can I integrate with custom tools?', a: 'Absolutely. Our platform includes a powerful API and webhook system to connect with any in-house or proprietary software.' },
			{ q: 'Is my data secure?', a: 'Security is our top priority. We are SOC 2 Type II certified and all data is encrypted in transit and at rest.' },
			{ q: 'Do you offer support?', a: 'Yes, we offer 24/7 email support on all plans, with dedicated phone and Slack support available on our Enterprise plan.' },
			{ q: 'Can I cancel at any time?', a: 'Yes, you can cancel your subscription at any time from your account dashboard. Your plan will remain active until the end of the current billing cycle.' }
		],
		finalCta: {
			hook: 'Ready to build your automated future?',
			cta: 'Start Automating Now'
		},
		footer: {
			copyright: `© ${new Date().getFullYear()} Silo Automation, Inc. All rights reserved.`,
			links: [
				{ text: 'Privacy Policy', href: '/legal/privacy' },
				{ text: 'Terms of Service', href: '/legal/terms' },
				{ text: 'Cookie Policy', href: '/legal/cookies' }
			],
			contact: 'support@silo-automation.com'
		}
	};

	// --- Lifecycle & Interactions ---
	onMount(() => {
		// Check for reduced motion preference
		const mediaQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
		prefersReducedMotion = mediaQuery.matches;
		mediaQuery.addEventListener('change', (e) => (prefersReducedMotion = e.matches));

		// Handle announcement bar persistence
		if (localStorage.getItem('announcementDismissed') === 'true') {
			showAnnouncement = false;
		}
	});

	function handleDismissAnnouncement() {
		showAnnouncement = false;
		localStorage.setItem('announcementDismissed', 'true');
	}

	function handleFaqToggle(e: MouseEvent) {
		const button = e.currentTarget as HTMLButtonElement;
		const content = button.nextElementSibling as HTMLElement;
		const isExpanded = button.getAttribute('aria-expanded') === 'true';

		button.setAttribute('aria-expanded', String(!isExpanded));
		if (!isExpanded) {
			content.style.maxHeight = content.scrollHeight + 'px';
		} else {
			content.style.maxHeight = '0px';
		}
	}
</script>

<svelte:head>
	<title>{content.title}</title>
	<meta name="description" content={content.metaDescription} />
	<link rel="canonical" href={content.canonicalUrl} />
	<!-- Open Graph -->
	<meta property="og:title" content={content.title} />
	<meta property="og:description" content={content.metaDescription} />
	<meta property="og:image" content={content.ogImageUrl} />
	<meta property="og:url" content={content.canonicalUrl} />
	<meta property="og:type" content="website" />
	<!-- JSON-LD -->
	<script type="application/ld+json">
		{
		  "@context": "https://schema.org",
		  "@type": "Organization",
		  "name": "${content.organization.name}",
		  "url": "${content.organization.url}",
		  "logo": "${content.organization.logo}"
		}
	</script>
	<script type="application/ld+json">
		{
		  "@context": "https://schema.org",
		  "@type": "Product",
		  "name": "${content.product.name}",
		  "description": "${content.product.description}",
		  "brand": {
			"@type": "Organization",
			"name": "${content.organization.name}"
		  }
		}
	</script>
</svelte:head>

<!-- Accessibility: Skip to main content -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Page Wrapper -->
<div class="landing-page">
	<!-- 1. Announcement Bar -->
	{#if showAnnouncement}
		<div class="announcement-bar">
			<p>
				{content.announcement.text}
				<a href="#">{content.announcement.cta} &rarr;</a>
			</p>
			<button
				aria-label="Dismiss announcement"
				on:click={handleDismissAnnouncement}
				on:keydown={(e) => e.key === 'Escape' && handleDismissAnnouncement()}
			>
				&times;
			</button>
		</div>
	{/if}

	<!-- 2. Header -->
	<header class="page-header">
		<div class="container">
			<a href="/" class="logo" aria-label="Homepage">
				<!-- Placeholder SVG Logo -->
				<svg width="40" height="40" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg"><rect width="100" height="100" rx="20" fill="currentColor"/></svg>
				<span>{content.organization.name}</span>
			</a>
			<nav aria-label="Primary">
				<ul>
					<li><a href="#features">Features</a></li>
					<li><a href="#pricing">Pricing</a></li>
					<li><a href="#faq">FAQ</a></li>
				</ul>
			</nav>
			<div class="header-actions">
				<a href="/login" class="cta-secondary">Log In</a>
				<a href="/signup" class="cta-primary">Get Started</a>
			</div>
		</div>
	</header>

	<main id="main-content">
		<!-- 3. Hero Section -->
		<section class="hero">
			<div class="container">
				<h1 class="hero-hook">{content.hero.hook}</h1>
				<p class="hero-sub-hook">{content.hero.subHook}</p>
				<div class="hero-ctas">
					<a href="/signup" class="cta-primary">{content.hero.primaryCta}</a>
					<a href="#demo" class="cta-secondary">{content.hero.secondaryCta}</a>
				</div>
				<ul class="hero-trust-cues">
					{#each content.hero.trustCues as cue}
						<li>{cue}</li>
					{/each}
				</ul>
			</div>
		</section>

		<!-- 4. Social Proof -->
		<section class="social-proof">
			<div class="container">
				<p>{content.socialProof.counts}</p>
				<div class="logo-strip">
					{#each content.socialProof.logos as logo}
						<img src={logo.src} alt="{logo.name} logo" loading="lazy" width="120" height="40" />
					{/each}
				</div>
			</div>
		</section>

		<!-- 5. Value Propositions -->
		<section class="value-props">
			<div class="container">
				<div class="section-header">
					<h2>Why Choose Us?</h2>
					<p>Unlock unparalleled efficiency and control.</p>
				</div>
				<div class="grid">
					{#each content.valueProps as prop, i}
						<div class="card">
							<h3>{prop.title}</h3>
							<p>{prop.description}</p>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- 6. Feature Grid -->
		<section id="features" class="feature-grid">
			<div class="container">
				<div class="section-header">
					<h2>Powerful Features, Effortless Control</h2>
					<p>Everything you need to automate and scale your business.</p>
				</div>
				{#each content.features as feature, i}
					<div class="feature-item" class:reverse={i % 2 !== 0}>
						<div class="feature-text">
							<h3>{feature.title}</h3>
							<p>{feature.description}</p>
							<a href="#" class="cta-link">Learn more &rarr;</a>
						</div>
						<div class="feature-visual">
							<img src={feature.image} alt="{feature.title} screenshot" loading="lazy" width="500" height="350" />
						</div>
					</div>
				{/each}
			</div>
		</section>

		<!-- 7. How It Works -->
		<section class="how-it-works">
			<div class="container">
				<div class="section-header">
					<h2>Get Started in 3 Simple Steps</h2>
				</div>
				<div class="steps-grid">
					{#each content.howItWorks as item, i}
						<div class="step-card">
							<div class="step-number">{item.step}</div>
							<h4>{item.title}</h4>
							<p>{item.description}</p>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- 8. Use Cases / Personas -->
		<section class="personas">
			<div class="container">
				<div class="section-header">
					<h2>Built for Every Team</h2>
					<p>Whatever your role, Silo Automation has a solution.</p>
				</div>
				<div class="grid">
					{#each content.personas as persona, i}
						<div class="card">
							<h4>{persona.persona}</h4>
							<p><strong>Problem:</strong> {persona.problem}</p>
							<p><strong>Outcome:</strong> {persona.outcome}</p>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- 9. Metrics / Outcomes -->
		<section class="metrics">
			<div class="container">
				<div class="section-header">
					<h2>Real Results, Backed by Data</h2>
				</div>
				<div class="metrics-grid">
					{#each content.metrics as metric, i}
						<div class="metric-item">
							<div class="metric-value">{metric.value}</div>
							<div class="metric-label">{metric.label}</div>
							<p class="metric-proof">{metric.proof}</p>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- 10. Integrations -->
		<section class="integrations">
			<div class="container">
				<div class="section-header">
					<h2>{content.integrations.text}</h2>
				</div>
				<div class="logo-strip">
					{#each content.integrations.logos as logo}
						<img src={logo.src} alt="{logo.name} logo" loading="lazy" width="64" height="64" />
					{/each}
				</div>
				<a href="/integrations" class="cta-link">See all integrations &rarr;</a>
			</div>
		</section>

		<!-- 11. Testimonials -->
		<section class="testimonials">
			<div class="container">
				<div class="section-header">
					<h2>What Our Customers Say</h2>
				</div>
				<div class="grid">
					{#each content.testimonials as testimonial, i}
						<blockquote class="card">
							<p>"{testimonial.quote}"</p>
							<footer>
								<cite>
									<strong>{testimonial.name}</strong>, {testimonial.title}
								</cite>
							</footer>
						</blockquote>
					{/each}
				</div>
			</div>
		</section>

		<!-- 12. Pricing Preview -->
		<section id="pricing" class="pricing-preview">
			<div class="container">
				<div class="section-header">
					<h2>{content.pricing.teaser}</h2>
				</div>
				<div class="pricing-box">
					<p>Our plans are designed to grow with you.</p>
					<div class="plan-price">{content.pricing.plan}</div>
					<a href="/pricing" class="cta-primary">{content.pricing.cta}</a>
				</div>
			</div>
		</section>

		<!-- 13. FAQ -->
		<section id="faq" class="faq">
			<div class="container">
				<div class="section-header">
					<h2>Frequently Asked Questions</h2>
				</div>
				<div class="faq-list">
					{#each content.faq as item, i}
						<div class="faq-item">
							<button
								class="faq-question"
								aria-expanded="false"
								aria-controls="faq-answer-{i}"
								on:click={handleFaqToggle}
							>
								<span>{item.q}</span>
								<span class="faq-icon">+</span>
							</button>
							<div id="faq-answer-{i}" class="faq-answer" role="region">
								<p>{item.a}</p>
							</div>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- 14. Final CTA -->
		<section id="demo" class="final-cta">
			<div class="container">
				<h2>{content.finalCta.hook}</h2>
				<a href="/signup" class="cta-primary">{content.finalCta.cta}</a>
			</div>
		</section>
	</main>

	<!-- 15. Footer -->
	<footer class="page-footer">
		<div class="container">
			<div class="footer-main">
				<div class="footer-about">
					<a href="/" class="logo" aria-label="Homepage">
						<svg width="32" height="32" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg"><rect width="100" height="100" rx="20" fill="currentColor"/></svg>
						<span>{content.organization.name}</span>
					</a>
					<p>&copy; {new Date().getFullYear()} {content.footer.copyright}</p>
					<p><a href="mailto:{content.footer.contact}">{content.footer.contact}</a></p>
				</div>
				<div class="footer-links">
					<h4>Company</h4>
					<ul>
						<li><a href="/about">About Us</a></li>
						<li><a href="/careers">Careers</a></li>
						<li><a href="/blog">Blog</a></li>
					</ul>
				</div>
				<div class="footer-links">
					<h4>Legal</h4>
					<ul>
						{#each content.footer.links as link}
							<li><a href={link.href}>{link.text}</a></li>
						{/each}
					</ul>
				</div>
			</div>
		</div>
	</footer>
</div>

<style lang="scss">
	.landing-page {
		animation: fadeIn 0.8s ease-in-out forwards;
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
	
	/* --- TOKENS (CSS Custom Properties) --- */
	:global(:root) {
		--c-primary: #007bff;
		--c-primary-dark: #0056b3;
		--c-secondary: #6c757d;
		--c-text: #212529;
		--c-text-light: #495057;
		--c-bg: #ffffff;
		--c-bg-alt: #f8f9fa;
		--c-border: #dee2e6;
		--c-white: #fff;
		--c-focus-ring: rgba(0, 123, 255, 0.5);

		--font-sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
		--font-serif: 'Georgia', serif;

		--space-xs: 0.25rem; // 4px
		--space-sm: 0.5rem; // 8px
		--space-md: 1rem; // 16px
		--space-lg: 2rem; // 32px
		--space-xl: 4rem; // 64px
		--space-xxl: 8rem; // 128px

		--radius-sm: 0.25rem;
		--radius-md: 0.5rem;
		--radius-lg: 1rem;

		--shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.05), 0 1px 2px rgba(0, 0, 0, 0.03);
		--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.07), 0 2px 4px rgba(0, 0, 0, 0.05);
		--shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.07), 0 4px 6px rgba(0, 0, 0, 0.06);

		--transition-fast: 200ms ease-in-out;
		--transition-normal: 300ms ease-in-out;
	}

	/* --- GLOBAL STYLES & RESETS --- */
	:global(body) {
		margin: 0;
		font-family: var(--font-sans);
		color: var(--c-text);
		background-color: var(--c-bg);
		line-height: 1.6;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}

	:global(h1, h2, h3, h4) {
		font-weight: 700;
		line-height: 1.2;
		margin-top: 0;
		margin-bottom: var(--space-md);
	}
	:global(h1) { font-size: clamp(2.5rem, 5vw, 3.5rem); }
	:global(h2) { font-size: clamp(2rem, 4vw, 2.75rem); }
	:global(h3) { font-size: 1.5rem; }
	:global(h4) { font-size: 1.2rem; }

	:global(p) {
		margin-top: 0;
		margin-bottom: var(--space-md);
	}

	:global(a) {
		color: var(--c-primary);
		text-decoration: none;
		transition: color var(--transition-fast);
		&:hover {
			color: var(--c-primary-dark);
			text-decoration: underline;
		}
	}

	/* --- UTILITIES --- */
	.container {
		width: 100%;
		max-width: 1200px;
		margin-left: auto;
		margin-right: auto;
		padding: 0 var(--space-lg);
	}

	.skip-link {
		position: absolute;
		top: -100px;
		left: 0;
		background: var(--c-primary);
		color: var(--c-white);
		padding: var(--space-md);
		z-index: 100;
		transition: top 0.3s;
		&:focus {
			top: 0;
		}
	}

	/* --- ATOMS: Buttons & Links --- */
	.cta-primary, .cta-secondary, .cta-link {
		display: inline-block;
		font-weight: 600;
		border-radius: var(--radius-md);
		padding: 0.75rem 1.5rem;
		text-align: center;
		transition: transform var(--transition-fast), box-shadow var(--transition-fast);
		border: 2px solid transparent;
		cursor: pointer;
		
		&:hover {
			transform: translateY(-2px);
			box-shadow: var(--shadow-md);
			text-decoration: none;
		}
		&:focus-visible {
			outline: 2px solid transparent;
			outline-offset: 2px;
			box-shadow: 0 0 0 3px var(--c-white), 0 0 0 5px var(--c-focus-ring);
		}
	}

	.cta-primary {
		background-color: var(--c-primary);
		color: var(--c-white);
		&:hover {
			background-color: var(--c-primary-dark);
			color: var(--c-white);
		}
	}

	.cta-secondary {
		background-color: var(--c-bg);
		color: var(--c-primary);
		border-color: var(--c-border);
		&:hover {
			background-color: var(--c-bg-alt);
			color: var(--c-primary-dark);
		}
	}

	.cta-link {
		padding: 0;
		font-weight: 600;
		color: var(--c-primary);
		&:hover {
			box-shadow: none;
			transform: none;
		}
	}

	/* --- ATOMS: Cards --- */
	.card {
		background: var(--c-white);
		border-radius: var(--radius-lg);
		padding: var(--space-lg);
		box-shadow: var(--shadow-md);
		transition: transform var(--transition-normal), box-shadow var(--transition-normal);
		height: 100%;
		&:hover {
			transform: translateY(-4px);
			box-shadow: var(--shadow-lg);
		}
	}

	/* --- ORGANISMS: Sections --- */
	section {
		padding: var(--space-xl) 0;
		@media (min-width: 768px) {
			padding: var(--space-xxl) 0;
		}
	}

	.section-header {
		text-align: center;
		margin-bottom: var(--space-xl);
		max-width: 700px;
		margin-left: auto;
		margin-right: auto;
		h2 {
			margin-bottom: var(--space-sm);
		}
		p {
			font-size: 1.125rem;
			color: var(--c-text-light);
		}
	}

	.grid {
		display: grid;
		gap: var(--space-lg);
		@media (min-width: 768px) {
			grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		}
	}

	/* 1. Announcement Bar */
	.announcement-bar {
		background-color: var(--c-primary);
		color: var(--c-white);
		padding: var(--space-sm) var(--space-lg);
		display: flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		position: relative;
		p {
			margin: 0;
			font-weight: 500;
		}
		a {
			color: var(--c-white);
			text-decoration: underline;
			margin-left: var(--space-sm);
		}
		button {
			background: none;
			border: none;
			color: var(--c-white);
			font-size: 1.5rem;
			line-height: 1;
			cursor: pointer;
			padding: 0 var(--space-md);
			position: absolute;
			right: var(--space-md);
			opacity: 0.8;
			&:hover {
				opacity: 1;
			}
		}
	}

	/* 2. Header */
	.page-header {
		background: var(--c-bg);
		padding: var(--space-md) 0;
		border-bottom: 1px solid var(--c-border);
		position: sticky;
		top: 0;
		z-index: 10;
		.container {
			display: flex;
			justify-content: space-between;
			align-items: center;
		}
		.logo {
			display: flex;
			align-items: center;
			gap: var(--space-sm);
			font-weight: 700;
			font-size: 1.25rem;
			color: var(--c-text);
			&:hover { text-decoration: none; }
			svg { color: var(--c-primary); }
		}
		nav {
			display: none;
			@media (min-width: 768px) {
				display: block;
			}
			ul {
				list-style: none;
				margin: 0;
				padding: 0;
				display: flex;
				gap: var(--space-lg);
			}
			a {
				color: var(--c-text-light);
				font-weight: 500;
				&:hover {
					color: var(--c-primary);
					text-decoration: none;
				}
			}
		}
		.header-actions {
			display: flex;
			align-items: center;
			gap: var(--space-sm);
		}
	}

	/* 3. Hero */
	.hero {
		text-align: center;
		padding-top: var(--space-xl);
		.container {
			max-width: 800px;
		}
		.hero-hook {
			margin-bottom: var(--space-md);
		}
		.hero-sub-hook {
			font-size: 1.25rem;
			color: var(--c-text-light);
			margin-bottom: var(--space-lg);
		}
		.hero-ctas {
			display: flex;
			justify-content: center;
			gap: var(--space-md);
			margin-bottom: var(--space-lg);
		}
		.hero-trust-cues {
			list-style: none;
			padding: 0;
			margin: 0;
			display: flex;
			justify-content: center;
			gap: var(--space-lg);
			font-size: 0.9rem;
			color: var(--c-text-light);
			li {
				position: relative;
				&:not(:last-child)::after {
					content: '•';
					position: absolute;
					right: calc(-1 * var(--space-lg) / 2);
					color: var(--c-border);
				}
			}
		}
	}

	/* 4. Social Proof */
	.social-proof {
		padding-top: 0;
		padding-bottom: var(--space-xl);
		.container {
			text-align: center;
		}
		p {
			font-weight: 500;
			color: var(--c-text-light);
			margin-bottom: var(--space-lg);
		}
		.logo-strip {
			display: flex;
			flex-wrap: wrap;
			justify-content: center;
			align-items: center;
			gap: var(--space-xl);
			img {
				max-height: 30px;
				width: auto;
				filter: grayscale(100%);
				opacity: 0.7;
				transition: var(--transition-normal);
				&:hover {
					filter: grayscale(0%);
					opacity: 1;
				}
			}
		}
	}

	/* 5. Value Props */
	.value-props {
		background-color: var(--c-bg-alt);
		.card {
			text-align: center;
			h3 { color: var(--c-primary); }
		}
	}

	/* 6. Feature Grid */
	.feature-item {
		display: grid;
		align-items: center;
		gap: var(--space-xl);
		margin-bottom: var(--space-xxl);
		@media (min-width: 768px) {
			grid-template-columns: 1fr 1fr;
		}
		&.reverse {
			.feature-text { order: 2; }
		}
		.feature-visual img {
			width: 100%;
			height: auto;
			border-radius: var(--radius-lg);
			box-shadow: var(--shadow-lg);
		}
	}

	/* 7. How It Works */
	.how-it-works {
		background-color: var(--c-bg-alt);
		.steps-grid {
			display: grid;
			gap: var(--space-lg);
			text-align: center;
			@media (min-width: 768px) {
				grid-template-columns: repeat(3, 1fr);
			}
		}
		.step-card {
			padding: var(--space-lg);
		}
		.step-number {
			width: 50px;
			height: 50px;
			border-radius: 50%;
			background: var(--c-primary);
			color: var(--c-white);
			display: grid;
			place-items: center;
			font-size: 1.5rem;
			font-weight: 700;
			margin: 0 auto var(--space-md);
		}
	}

	/* 9. Metrics */
	.metrics {
		background-color: var(--c-primary);
		color: var(--c-white);
		.section-header h2, .section-header p {
			color: var(--c-white);
		}
		.metrics-grid {
			display: grid;
			gap: var(--space-xl);
			text-align: center;
			@media (min-width: 768px) {
				grid-template-columns: repeat(3, 1fr);
			}
		}
		.metric-value {
			font-size: clamp(3rem, 6vw, 5rem);
			font-weight: 700;
			line-height: 1;
		}
		.metric-label {
			font-size: 1.25rem;
			font-weight: 500;
			margin-bottom: var(--space-sm);
		}
		.metric-proof {
			font-size: 0.9rem;
			opacity: 0.8;
			margin: 0;
		}
	}

	/* 10. Integrations */
	.integrations {
		.container { text-align: center; }
		.logo-strip {
			display: flex;
			flex-wrap: wrap;
			justify-content: center;
			align-items: center;
			gap: var(--space-xl);
			margin-bottom: var(--space-lg);
			img {
				height: 48px;
				width: auto;
				transition: transform var(--transition-fast);
				&:hover {
					transform: scale(1.1);
				}
			}
		}
	}

	/* 11. Testimonials */
	.testimonials {
		background-color: var(--c-bg-alt);
		blockquote {
			margin: 0;
			p {
				font-size: 1.125rem;
				font-style: italic;
			}
			cite {
				font-style: normal;
				color: var(--c-text-light);
			}
		}
	}

	/* 12. Pricing Preview */
	.pricing-preview {
		.pricing-box {
			max-width: 500px;
			margin: 0 auto;
			text-align: center;
			padding: var(--space-xl);
			border: 1px solid var(--c-border);
			border-radius: var(--radius-lg);
			box-shadow: var(--shadow-md);
		}
		.plan-price {
			font-size: 2rem;
			font-weight: 700;
			margin: var(--space-md) 0;
			color: var(--c-primary);
		}
	}

	/* 13. FAQ */
	.faq {
		.faq-list {
			max-width: 800px;
			margin: 0 auto;
		}
		.faq-item {
			border-bottom: 1px solid var(--c-border);
		}
		.faq-question {
			width: 100%;
			background: none;
			border: none;
			text-align: left;
			padding: var(--space-lg) 0;
			font-size: 1.2rem;
			font-weight: 600;
			cursor: pointer;
			display: flex;
			justify-content: space-between;
			align-items: center;
			gap: var(--space-md);
			.faq-icon {
				font-size: 1.5rem;
				transition: transform var(--transition-fast);
			}
			&[aria-expanded='true'] .faq-icon {
				transform: rotate(45deg);
			}
		}
		.faq-answer {
			max-height: 0;
			overflow: hidden;
			transition: max-height var(--transition-normal);
			p {
				padding-bottom: var(--space-lg);
				color: var(--c-text-light);
			}
		}
	}

	/* 14. Final CTA */
	.final-cta {
		background-color: var(--c-primary);
		color: var(--c-white);
		text-align: center;
		h2 {
			color: var(--c-white);
			margin-bottom: var(--space-lg);
		}
		.cta-primary {
			background-color: var(--c-white);
			color: var(--c-primary);
			&:hover {
				background-color: var(--c-bg-alt);
			}
		}
	}

	/* 15. Footer */
	.page-footer {
		background-color: var(--c-text);
		color: var(--c-bg-alt);
		padding: var(--space-xl) 0;
		font-size: 0.9rem;
		a {
			color: var(--c-bg-alt);
			&:hover {
				color: var(--c-white);
			}
		}
		.footer-main {
			display: grid;
			gap: var(--space-xl);
			@media (min-width: 768px) {
				grid-template-columns: 2fr 1fr 1fr;
			}
		}
		.logo {
			color: var(--c-white);
			margin-bottom: var(--space-md);
			svg { color: var(--c-primary); }
		}
		.footer-links {
			h4 {
				color: var(--c-white);
				margin-bottom: var(--space-md);
			}
			ul {
				list-style: none;
				padding: 0;
				margin: 0;
				li {
					margin-bottom: var(--space-sm);
				}
			}
		}
	}
</style>
