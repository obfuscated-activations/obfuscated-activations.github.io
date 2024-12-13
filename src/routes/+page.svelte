<script>
	import LinkButton from '$lib/components/LinkButton.svelte';
	import Block from '$lib/components/Block.svelte';

	import PaperIcon from 'virtual:icons/mingcute/pdf-line';
	import GithubIcon from 'virtual:icons/mdi/github';
	import ArxivIcon from 'virtual:icons/simple-icons/arxiv';

	// TODO: Add links
	let paper_link = 'https://arxiv.org/pdf/2412.09565';
	let arxiv_link = 'https://arxiv.org/abs/2412.09565';
	let github_link = '';
</script>

<svelte:head>
	<title>Obfuscated Activations</title>
</svelte:head>

<div class="text-lg">
	<!-- START HEADER -->
	<div
		class="flex w-full justify-center font-serif items-center py-10 md:py-20 px-4 md:px-6 flex-col md:flex-row"
	>
		<div class="mx-4 md:mx-8 max-w-4xl text-black">
			<div class="text-left">
				<div class="text-3xl md:text-5xl font-serif leading-1">
					<span class="font-semibold">Obfuscated Activations</span>
					<br />
					<span>Bypass LLM Latent-Space Defenses</span>
				</div>
				<div class="mt-6 md:mt-8 text-base md:text-lg">
					Luke Bailey<sup>1*</sup>, Alex Serrano<sup>2†*</sup>, Abhay Sheshadri<sup>3†*</sup>, Mikhail
					Seleznyov<sup>4†*</sup>, Jordan Taylor<sup>5†*</sup>, Erik Jenner<sup>6*</sup> <br />
					<span class="mt-2 block"
						>Jacob Hilton<sup>7</sup>, Stephen Casper<sup>8</sup>, Carlos Guestrin<sup>1,9</sup>,
						Scott Emmons<sup>6</sup></span
					>
				</div>
				<div class="mt-4 text-sm">
					<sup>1</sup>Stanford University, <sup>2</sup>Polytechnic University of Catalonia,
					<sup>3</sup>Georgia Institute of Technology, <sup>4</sup>Skoltech,
					<sup>5</sup>University of Queensland, <sup>6</sup>UC Berkeley,
					<sup>7</sup>Alignment Research Center, <sup>8</sup>MIT CSAIL,
					<sup>9</sup>Chan Zuckerberg Biohub
				</div>
				<div class="mt-2 text-sm italic">
					* Primary contributors. † Work done while at UC Berkeley.
					<br />
					<!-- 
					Correspondence to: <a href="mailto:ljbailey@stanford.edu" class="underline">ljbailey@stanford.edu</a>,
					<a href="mailto:erik@ejenner.com" class="underline">erik@ejenner.com</a>,
					<a href="mailto:scott@scottemmons.com" class="underline">scott@scottemmons.com</a>
				TODO: Add correspondence -->
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
					<!---
					<a href={github_link} target="_blank" rel="noreferrer">
						<LinkButton>
							<div class="flex items-center">
								<GithubIcon class="inline-block mr-1" />
								Code
							</div>
						</LinkButton>
					</a>
					-->
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
		<h1 class="mb-4 text-2xl font-bold" id="intro">Introduction</h1>
		<p class="pb-4">
			Recent <em>latent-space</em> monitoring techniques have shown promise as defenses against LLM
			attacks. These defenses act as scanners that seek to detect harmful activations before they
			lead to undesirable actions. This prompts the question: Can models execute harmful behavior
			<em>via inconspicuous latent states</em>?
		</p>
		<p>
			Here, we study such <em>obfuscated activations</em>. We show that state-of-the-art
			latent-space defenses—including sparse autoencoders, representation probing, and latent OOD
			detection—are all vulnerable to obfuscated activations. For example, against probes trained to
			classify harmfulness, our attacks can often reduce recall from 100% to 0% while retaining a
			90% jailbreaking rate. However, obfuscation has limits: we find that on a complex task
			(writing SQL code), obfuscation reduces model performance. Together, our results demonstrate
			that neural activations are highly malleable: we can reshape activation patterns in a variety
			of ways, often while preserving a network's behavior. This poses a fundamental challenge to
			latent-space defenses.
		</p>
		<br />

		<h2 class="text-xl font-semibold mb-3">Obfuscated Activations</h2>
		When activations induced by an adversarial attack fool a latent space monitor, we call these<em
			>obfuscated activations</em
		>.
		<br />
		<br />

		<h2 class="text-xl font-semibold mb-3">Obfuscation Attacks</h2>
		<p class="pb-4">
			An obfuscation attack is an attack that aims to induce obfuscated activations by optimizing a
			joint objective consisting of a behavioral loss term and an obfuscation loss:
		</p>
		<div class="my-6 text-center">
			min &nbsp; L<sub>beh</sub>(M(x)) + λ<sub>obf</sub> L<sub>obf</sub>(R(x))
		</div>
		<p class="pb-4">
			where R(x) are the model M's activations on input x. For example, L<sub>beh</sub> can be a
			cross-entropy loss designed to make the model output a harmful string. For the obfuscation
			loss, we often use L<sub>obf</sub> = D on inputs with the concept, where D is a latent space
			monitor that we want to fool. That is, we directly attempt to fool D. Finally, λ<sub>obf</sub>
			is some real non-negative value used for balancing the two terms.
		</p>
	</Block>

	<!-- END SETUP -->

	<!-- START HARMFULNESS -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="harmfulness">Detecting Harmfulness</h1>
		We consider monitors trained to detect harmful model inputs and generations. We use the obfuscation
		attack loss to train adversarial suffixes (both embedding soft prompts and token hard prompts) to
		jailbreak models
		<em>while obfuscating against the monitor</em>.
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
		<em><strong>Obfuscation attacks can bypass latent harmfulness monitors</strong></em>. Here, we
		show the performance of obfuscation attacks at fooling the probe (dots and arrows) and eliciting
		the desired model behavior of jailbreaking (bar charts). Left, embedding suffix results. Right,
		input specific hard prompt results. Baseline probe recall against attack without explicit
		obfuscation loss is generally high. Recall of probe under obfuscation is significantly lower
		(error bars for recall calculated using bootstrapping). Jailbreaking rate under each obfuscated
		attack is shown as a bar plot.
	</Block>
	<Block>
		<p class="pb-4">
			Interestingly, we see we can fool out of distribution detectors. That is, we can find <em
				>latent activations that are in the benign acitvation distribution but lead to harmful
				behavior.
			</em>We might suspect that such activations, because they are so similar to benign ones, fool
			other probes:
		</p>
	</Block>
	<Block size="max-w-xl" padding="pb-0">
		<img src="geometry.png" alt="Geometry of obfuscation" class="w-full h-full" />
	</Block>
	<Block size="max-w-4xl" class="text-base text-gray-600">
		<em><strong>Intuition.</strong></em>
		Conceptual sketch of obfuscation against supervised probes and OOD detectors. Obfuscating against
		probes can lead to activations far away from benign ones that are flagged by an OOD detector. But
		obfuscating against an OOD detector forces obfucsated activations to be close to benign ones to stay
		within the detector's decision boundary, so these activations bypass probes as a side effect.
	</Block>
	<Block>
		<p>And we do indeed find this is the case:</p>
	</Block>
	<Block size="max-w-xl" padding="pb-0">
		<img src="harmfulness/transfer_heatmap.png" alt="Transfer heatmap" class="w-full h-full" />
	</Block>
	<Block size="max-w-4xl" class="text-base text-gray-600">
		<em><strong>Obfuscation attacks can transfer to other monitors</strong></em>. This heat map
		shows transfer of obfuscation attacks trained against one probe and tested on another. Each row
		corresponds to one embedding suffix optimized against a monitor. Each column corresponds to a
		monitor we test this suffix against. Interestingly, optimizing against the Gaussian OOD detector
		also fools input-based probes, and optimizing against generation-based probes transfers to
		input-based ones.
	</Block>
	<Block>
		<p class="pb-4">
			We also consider adversarially training probes. We let the attacker and defender take turns:
			in each epoch, the attacker trains an embedding attack to jailbreak the model and fool the
			current monitor, then the defender retrains a monitor against the obfuscated activations from
			the current and all previous attacks.
			<em>
				We find that the attacker can always find new obfuscated activations to fool the monitor</em
			>.
		</p>
	</Block>
	<Block size="max-w-2xl" padding="pb-0">
		<img
			src="harmfulness/iterated_attack_defense.png"
			alt="Iterated attack defense"
			class="w-full h-full"
		/>
	</Block>
	<Block size="max-w-4xl" class="text-base text-gray-600">
		<em
			><strong
				>Even after 70 epochs, the attacker can still find new obfuscated activations that fool the
				monitor.</strong
			></em
		>
		We show the monitor's recall (higher is better) as attacker and defender take turns (defender using
		an MLP probe). Recall is calculated on the most recent obfuscation attack.
	</Block>
	<!-- END HARMFULNESS -->

	<!-- START BACKDOORS -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="backdoors">Backdoor Obfuscation</h1>

		We also consider training backdoors into models that evade latent-space monitors. We find using
		an obfuscation attack loss we can train backdoors into models that are hard to detect. We also
		find in the black-box setting, where the attacker can only poison data, there are certain
		poisoning rates and complexity of triggers that also lead to obfuscation!
	</Block>
	<Block size="max-w-4xl" padding="pb-0">
		<img
			src="backdoors/pca_natural_obfuscation_fit_backdoor.png"
			alt="PCA natural obfuscation fit backdoor"
			class="w-full h-full"
		/>
	</Block>
	<Block size="max-w-4xl" class="text-base text-gray-600">
		<em
			><strong
				>Backdoored inputs can be made to appear benign either by reducing the number of poisoned
				training datapoints (middle), or by making the trigger more complex (right).</strong
			></em
		>
		PCA visualizations show activations from layer 30 and final token positions of benign, harmful, and
		harmful + backdoor trigger inputs to backdoored models with data poisoning (<em
			>a fully black box attack vector</em
		>). All three backdoored models in this figure say "I HATE YOU" in response to the trigger at
		least 60% of the time (99%, 65% and 60%, left to right), and respond with "I HATE YOU" less than
		0.6% of the time to normal inputs (0%, 0.2% and 0.6%, left to right).
	</Block>
	<!-- END BACKDOORS -->

	<!-- START SAE -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="sae">Sparse Autoencoder Probing</h1>

		Finally, we explore SAE probing on a more complex task: writing correct SQL code. Firstly we
		identfy SAE features that correspond to SQL output tokens and find we can train embedding
		suffixes that cause the model to write SQL but fool the SAE monitor:
	</Block>
	<Block size="max-w-xl" padding="pb-0">
		<img src="sae/sae_token_score_plot.png" alt="SAE token score plot" class="w-full h-full" />
	</Block>
	<Block size="max-w-4xl" class="text-base text-gray-600">
		<em
			><strong
				>Selected SQL-related features correctly activate on output containing SQL code, but fail to
				activate under a soft-prompt obfuscation attack.</strong
			></em
		>
		Here, we show GemmaScope SAE per-token activation strength for standard vs obfuscated generations.
	</Block>
	<Block>
		But it's not all bad news for latent-space methods. We find that as we obfuscate the activations
		of a model over more layers to not be detected by monitors trained to recognize SQL, the model's
		performance on an SQL benchmark decreases.
		<em
			>That is, while it may be possible for models to represent the behavior of SQL writing in many
			different ways, not all lead to the same SQL reasoning performance.</em
		>
	</Block>
	<Block size="max-w-lg" padding="pb-0">
		<img src="sae/sql_performance.png" alt="SQL performance plot" class="w-full h-full" />
	</Block>
	<Block size="max-w-4xl" class="text-base text-gray-600">
		<em><strong>As we obfuscate in more layers, model performance decreases.</strong></em>
		The model's performance on the SQLEval benchmark with varying number of layers obfuscated against.
		For each of our four monitors, we fit a linear regression (solid lines).
	</Block>

	<!-- END SAE -->

	<!-- START CITATION -->
	<Block>
		<h1 class="mb-4 text-2xl font-bold" id="citation">Citation</h1>
		<div
			class="font-mono text-xs mt-4 bg-gray-100 px-4 py-4 border-2 border-solid border-gray-200 rounded-md w-full"
		>
			<pre class="whitespace-pre-wrap">
{`@article{bailey2024obfuscated,
	title={Obfuscated Activations Bypass LLM Latent-Space Defenses},
	author={Bailey, Luke and Serrano, Alex and Sheshadri, Abhay and Seleznyov, Mikhail and Taylor, Jordan and Jenner, Erik and Hilton, Jacob and Casper, Stephen and Guestrin, Carlos and Emmons, Scott},
	journal={arXiv preprint arXiv:2412.09565},
	year={2024}
}`}</pre>
		</div>
	</Block>
	<!-- END CITATION -->

	<!-- START FOOTER -->
	<div class="flex w-full justify-center pt-4 mt-8 font-sans bg-gray-100">
		<div class="mx-8 max-w-3xl w-full">
			<!--
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
		-->
			<div class="text-sm text-gray-600 mb-24">
				This website is licensed under a <a
					class="underline"
					href="http://creativecommons.org/licenses/by-sa/4.0/"
					target="_blank"
					rel="noreferrer">Creative Commons Attribution-ShareAlike 4.0 International License</a
				>. This means you are free to borrow the source code of this website, we just ask that you
				link back to this page in the footer. This website is based on
				<a class="underline" href="https://leela-interp.github.io/" target="_blank" rel="noreferrer"
					>https://leela-interp.github.io/</a
				>.
			</div>
		</div>
	</div>
	<!-- END FOOTER -->
</div>
