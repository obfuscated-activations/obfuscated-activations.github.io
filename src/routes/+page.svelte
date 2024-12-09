<script>
	import LinkButton from '$lib/components/LinkButton.svelte';
	import Block from '$lib/components/Block.svelte';

	import PaperIcon from 'virtual:icons/mingcute/pdf-line';
	import GithubIcon from 'virtual:icons/mdi/github';
	import ArxivIcon from 'virtual:icons/simple-icons/arxiv';

	// TODO: Add links
	let paper_link = '';
	let arxiv_link = '';
	let github_link = '';
</script>

<svelte:head>
	<title>Obfuscated Representations</title>
</svelte:head>

<div class="text-lg">
	<!-- START HEADER -->
	<div
		class="flex w-full justify-center font-serif items-center py-10 md:py-20 px-4 md:px-6 flex-col md:flex-row"
	>
		<div class="mx-4 md:mx-8 max-w-4xl text-black">
			<div class="text-left">
				<div class="text-3xl md:text-5xl font-serif leading-1">
					<span class="font-semibold">Obfuscated</span>
					<br />
					<span class="font-semibold">Representations</span>
					<br />
					<span>Bypass</span>
					<br />
					<span>Latent-Space Defenses</span>
				</div>
				<div class="mt-6 md:mt-8 text-base md:text-lg">
					Author 1<sup>1</sup>, Author 2<sup>1</sup>, Author 3<sup>1</sup>, Author 4<sup>1</sup>,
					Author 5<sup>1</sup>, Author 6<sup>1</sup>
				</div>
				<div class="mt-2 text-base">
					<sup>1</sup>UC Berkeley, <sup>2</sup>Stanford, <sup>3</sup>MIT
				</div>
				<div class="flex mt-8 space-x-4">
					<a href={paper_link}>
						<LinkButton>
							<div class="flex items-center">
								<PaperIcon class="inline-block mr-1" />
								Paper
							</div>
						</LinkButton>
					</a>
					<a href={arxiv_link}>
						<LinkButton>
							<div class="flex items-center">
								<ArxivIcon class="inline-block mr-1" />
								arXiv
							</div>
						</LinkButton>
					</a>
					<a href={github_link} target="_blank" rel="noreferrer">
						<LinkButton>
							<div class="flex items-center">
								<GithubIcon class="inline-block mr-1" />
								Code
							</div>
						</LinkButton>
					</a>
				</div>
			</div>
		</div>
		<div class="mx-4 md:mx-8 max-w-xl md:max-w-xl max-h-[500px] md:max-h-[600px] mt-8 md:mt-0">
			<img
				src="figure_1.png"
				alt="Diagram showing obfuscation attack concept"
				class="object-contain h-full w-full"
			/>
		</div>
	</div>
	<div class="w-full border-b border-gray-300"></div>
	<!-- END HEADER -->

	<!-- START INTRO/ABSTRACT-->
	<Block padding="pb-12 pt-10">
		<p class="pb-4">
			To defend against attacks on large language models (LLMs), there has been increasing interest
			in latent-space monitoring techniques that flag undesired behavior using the LLM's internal
			activations. Are these latent-space monitors fundamentally more robust than traditional
			defenses, or are they also adversarially vulnerable?
		</p>
		<p>
			To study this, we stress-test state-of-the-art latent monitors using targeted methods we call
			<q>obfuscation attacks</q>. In our experiments, all defenses can be fooled by these attacks,
			including probing, sparse autoencoders, representation rerouting, and latent anomaly
			detection. We call this phenomenon <q>obfuscated representations</q> - neural representations that
			make a network execute some behavior while evading monitors meant to detect this behavior. Obfuscated
			representations pose a key challenge to latent monitoring and demonstrate broad limitations in
			existing techniques.
		</p>
	</Block>
	<!-- END INTRO/ABSTRACT -->

	<!-- START SETUP -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="setup">Setup and method</h1>
		<p class="pb-4">
			Lorem ipsum odor amet, consectetuer adipiscing elit. Feugiat rhoncus commodo duis litora metus
			duis vivamus etiam. Ridiculus curae tortor aliquam nostra id tempus inceptos. Feugiat etiam
			vivamus cras suscipit dolor leo magna. Ad lacinia potenti class enim praesent lobortis nam
			vulputate. Nascetur maximus tempor finibus fusce a. Cursus et pretium urna ligula ex pulvinar
			arcu sodales.
		</p>
		<p>
			Vel potenti himenaeos cubilia aliquam id orci. Pulvinar habitasse risus sem gravida nec
			habitasse, ultrices leo. Ipsum aptent velit maximus nostra sem ultricies aenean. Cras justo
			primis consectetur cubilia hac libero. Suspendisse dolor curae netus porttitor suspendisse,
			elit imperdiet. Facilisi hendrerit turpis facilisi netus aptent placerat. Est euismod sit
			varius sagittis magna euismod. Curae varius sit curabitur sociosqu curae, tempus facilisi
			ligula. Ac id donec condimentum senectus sem tristique rutrum.
		</p>
	</Block>
	<!-- END SETUP -->

	<!-- START HARMFULNESS -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="harmfulness">Detecting Harmfulness</h1>
		Lorem ipsum odor amet, consectetuer adipiscing elit. Feugiat rhoncus commodo duis litora metus duis
		vivamus etiam. Ridiculus curae tortor aliquam nostra id tempus inceptos. Feugiat etiam vivamus cras
		suscipit dolor leo magna. Ad lacinia potenti class enim praesent lobortis nam vulputate. Nascetur
		maximus tempor finibus fusce a. Cursus et pretium urna ligula ex pulvinar arcu sodales.
	</Block>
	<Block size="max-w-5xl" padding="pb-0">
		<div class="flex flex-col md:flex-row gap-4">
			<div class="flex-1">
				<img
					src={'harmfulness/adaptive_obfuscation.png'}
					alt="Adaptive obfuscation"
					class="w-full h-full transition-all opacity-100"
				/>
			</div>
			<div class="flex-1">
				<img
					src={'harmfulness/hard_prompt_obfuscation.png'}
					alt="Hard prompt obfuscation"
					class="w-full h-full transition-all opacity-100"
				/>
			</div>
		</div>
	</Block>
	<Block size="max-w-4xl" class="text-base text-gray-600">
		<em><strong>Top row:</strong></em> The impact of activation patching on one square and in one
		layer at a time in an example puzzle. Darker squares mean that patching on that square had a
		higher impact on the output. The 3rd move target square (<span style="color: #0984e3"
			>blue dot</span
		>) is very important in layer 10 (middle board) in some puzzles.
		<em><strong>Bottom row:</strong></em> Average effects over 22k puzzles. Around layer 10, the
		effect of patching on the 3rd move target (<span style="color: #0984e3">blue line</span>) is big
		compared to most other squares (the gray line is the
		<em>maximum</em> effect over all other squares than the 1st/3rd move target and corrupted square(s).).
	</Block>
	<Block>
		<p class="pb-4">
			Convallis justo eget placerat eu nec massa ligula cras auctor. Mollis neque penatibus
			imperdiet mi est class massa. Vel mattis sapien ac pharetra curabitur sed quisque. Dictum
			laoreet tortor vehicula dapibus accumsan proin taciti.
		</p>
		<p>
			Fermentum a hendrerit habitasse odio eget vel. Scelerisque quam a tempor litora praesent.
			Suscipit praesent. Suscipit egestas euismod condimentum nibh scelerisque. Eget non vivamus
			tristique natoque aliquet curae ad mattis. Rhoncus imperdiet semper mauris semper; lobortis
			ullamcorper. Natoque blandit gravida neque imperdiet neque nullam tristique?
		</p>
	</Block>
	<Block size="max-w-xl" padding="pb-0">
		<img src="harmfulness/transfer_heatmap.png" alt="Transfer heatmap" class="w-full h-full" />
	</Block>
	<Block size="max-w-xl" class="text-base text-gray-600">
		<em><strong>Top row:</strong></em> The impact of activation patching on one square and in one
		layer at a time in an example puzzle. Darker squares mean that patching on that square had a
		higher impact on the output. The 3rd move target square (<span style="color: #0984e3"
			>blue dot</span
		>) is very important in layer 10 (middle board) in some puzzles.
	</Block>
	<Block>
		<p class="pb-4">
			Convallis justo eget placerat eu nec massa ligula cras auctor. Mollis neque penatibus
			imperdiet mi est class massa. Vel mattis sapien ac pharetra curabitur sed quisque. Dictum
			laoreet tortor vehicula dapibus accumsan proin taciti.
		</p>
		<p>
			Fermentum a hendrerit habitasse odio eget vel. Scelerisque quam a tempor litora praesent.
			Suscipit praesent. Suscipit egestas euismod condimentum nibh scelerisque. Eget non vivamus
			tristique natoque aliquet curae ad mattis. Rhoncus imperdiet semper mauris semper; lobortis
			ullamcorper. Natoque blandit gravida neque imperdiet neque nullam tristique?
		</p>
	</Block>
	<Block size="max-w-2xl" padding="pb-0">
		<img
			src="harmfulness/iterated_attack_defense.png"
			alt="Iterated attack defense"
			class="w-full h-full"
		/>
	</Block>
	<Block size="max-w-2xl" class="text-base text-gray-600">
		<em><strong>Top row:</strong></em> The impact of activation patching on one square and in one
		layer at a time in an example puzzle. Darker squares mean that patching on that square had a
		higher impact on the output. The 3rd move target square (<span style="color: #0984e3"
			>blue dot</span
		>) is very important in layer 10 (middle board) in some puzzles.
	</Block>
	<!-- END HARMFULNESS -->

	<!-- START BACKDOORS -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="backdoors">Backdoor Obfuscation</h1>
		Lorem ipsum odor amet, consectetuer adipiscing elit. Feugiat rhoncus commodo duis litora metus duis
		vivamus etiam. Ridiculus curae tortor aliquam nostra id tempus inceptos. Feugiat etiam vivamus cras
		suscipit dolor leo magna. Ad lacinia potenti class enim praesent lobortis nam vulputate. Nascetur
		maximus tempor finibus fusce a. Cursus et pretium urna ligula ex pulvinar arcu sodales.
	</Block>
	<Block size="max-w-4xl" padding="pb-0">
		<img
			src="backdoors/pca_natural_obfuscation_fit_backdoor.png"
			alt="PCA natural obfuscation fit backdoor"
			class="w-full h-full"
		/>
	</Block>
	<Block size="max-w-4xl" class="text-base text-gray-600">
		<em><strong>Top row:</strong></em> The impact of activation patching on one square and in one
		layer at a time in an example puzzle. Darker squares mean that patching on that square had a
		higher impact on the output. The 3rd move target square (<span style="color: #0984e3"
			>blue dot</span
		>) is very important in layer 10 (middle board) in some puzzles.
	</Block>
	<Block>
		<p class="pb-4">
			Convallis justo eget placerat eu nec massa ligula cras auctor. Mollis neque penatibus
			imperdiet mi est class massa. Vel mattis sapien ac pharetra curabitur sed quisque. Dictum
			laoreet tortor vehicula dapibus accumsan proin taciti.
		</p>
		<p>
			Lorem ipsum odor amet, consectetuer adipiscing elit. Feugiat rhoncus commodo duis litora metus
			duis vivamus etiam. Ridiculus curae tortor aliquam nostra id tempus inceptos. Feugiat etiam
			vivamus cras suscipit dolor leo magna. Ad lacinia potenti class enim praesent lobortis nam
			vulputate. Nascetur maximus tempor finibus fusce a. Cursus et pretium urna ligula ex pulvinar
			arcu sodales.
		</p>
	</Block>
	<!-- END BACKDOORS -->

	<!-- START SAE -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="sae">Sparse Autoencoder Probing</h1>
		Lorem ipsum odor amet, consectetuer adipiscing elit. Feugiat rhoncus commodo duis litora metus duis
		vivamus etiam. Ridiculus curae tortor aliquam nostra id tempus inceptos. Feugiat etiam vivamus cras
		suscipit dolor leo magna. Ad lacinia potenti class enim praesent lobortis nam vulputate. Nascetur
		maximus tempor finibus fusce a. Cursus et pretium urna ligula ex pulvinar arcu sodales.
	</Block>
	<Block size="max-w-xl" padding="pb-0">
		<img src="sae/sae_token_score_plot.png" alt="SAE token score plot" class="w-full h-full" />
	</Block>
	<Block size="max-w-xl" class="text-base text-gray-600">
		<em><strong>Top row:</strong></em> The impact of activation patching on one square and in one
		layer at a time in an example puzzle. Darker squares mean that patching on that square had a
		higher impact on the output. The 3rd move target square (<span style="color: #0984e3"
			>blue dot</span
		>) is very important in layer 10 (middle board) in some puzzles.
	</Block>
	<Block>
		Convallis justo eget placerat eu nec massa ligula cras auctor. Mollis neque penatibus imperdiet
		mi est class massa. Vel mattis sapien ac pharetra curabitur sed quisque. Dictum laoreet tortor
		vehicula dapibus accumsan proin taciti.
	</Block>
	<!-- END SAE -->

	<!-- START CITATION -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="citation">Citation</h1>
		<div
			class="font-mono text-xs mt-4 bg-gray-100 px-4 py-4 border-2 border-solid border-gray-200 rounded-md w-full"
		>
			<pre class="whitespace-pre-wrap">
{`@misc{citation here}`}</pre>
		</div>
	</Block>
	<!-- END CITATION -->

	<!-- START FOOTER -->
	<div class="flex w-full justify-center pt-4 mt-8 font-sans bg-gray-100">
		<div class="mx-8 max-w-3xl w-full">
			<div class="w-full flex justify-start items-center flex-col">
				<div class="text-gray-500 mt-4 text-2xl mb-8">
					<a href={paper_link} target="_blank" rel="noreferrer" class="mr-2">
						<ArxivIcon class="inline-block hover:text-black" />
					</a>
					<a href={github_link} target="_blank" rel="noreferrer" class="mr-2">
						<GithubIcon class="inline-block hover:text-black" />
					</a>
				</div>
			</div>
			<div class="text-sm text-gray-600 mb-24">
				This website is licensed under a <a
					class="underline"
					href="http://creativecommons.org/licenses/by-sa/4.0/"
					target="_blank"
					rel="noreferrer">Creative Commons Attribution-ShareAlike 4.0 International License</a
				>. This means you are free to borrow the source code of this website, we just ask that you
				link back to this page in the footer.
			</div>
		</div>
	</div>
	<!-- END FOOTER -->
</div>
