<script>
	import Sidebar from '$lib/utilities/Sidebar.svelte';
	import ChangelogLine from '$lib/utilities/ChangelogLine.svelte';
	import { Accordion, AccordionItem } from "carbon-components-svelte";

</script>

<svelte:head>
    <title>Updates & FAQ - F.H Tools</title>
</svelte:head>

<Sidebar selected="changelog">
	<main slot="container">
		<div class="mx-auto max-w-7xl">
			<section>
				<h2 class="text-xl bg-[#f4f4f4] p-2 mb-2 font-semibold">Frequently Asked Questions</h2>
				<Accordion>
					<AccordionItem title="How does the Citation Builder work?">
						<p>
						To use the citation builder, fill each of the relevant fields. As you do so, you will see the citation update in the grey box underneath the citation builder. Once you're done with creating your citation, click on the grey box that contains that citation and it will be copied to your clipboard.
						</p>
					</AccordionItem>
					<AccordionItem title="Can I see a history of the citations I create?">
						<p>
						No. This site doesn't store any data to avoid having to deal with databases and servers, and in order to keep this site free and maintainable. Therefore, I have no way of keeping track of the citations you create. All data that you may enter on the site is cleared when you leave the site.
						</p>
					</AccordionItem>
					<AccordionItem title="Can I request you add new features?">
						<p>
						Of course! My goal is to make sure that this website becomes as useful of a tool as possible for anyone interested in Family History, especially students. I would love to hear feedback on the kinds of features that would be useful to you. The best way to reach me is by email at <a class="text-sky-500 hover:text-sky-600 hover:underline" href="mailto:agbonnyh@gmail.com">agbonnyh@gmail.com</a>. Just two caveats. This is a side project that I work on in my (very limited) free time, so there may be some features that take a long time to be implemented or that I don't have the bandwidth to create and maintain. Also, I'm not being paid for this website meaning that some features may not be feasible because of the costs that would be associated with maintaining them.
						</p>
					</AccordionItem>
				</Accordion>
			<section class="mt-4">
				<h2 class="text-xl bg-[#f4f4f4] p-2 font-semibold">Changelog</h2>
				<hr/>
				<div>
					<ChangelogLine
							date="August 19, 2023"
							lines={[
								{type: "new", text: "Added a \"Clear Form\" button at the bottom of every citation template"},
								{type: "improvement", text: "Added an international option for all citations requiring an address"},
								{type: "change", text: "Switched from a custom algorithm for Soundex conversion to the open source words/soundex-code library"},
								{type: "change", text: "Combined the Church and Civil Record Templates"},
								{type: "change", text: "Removed sample data to make it easier to start inputting your template"}
						]}
					/>
					<ChangelogLine
						date="July 10, 2023"
						lines={[
							{type: "bug", text: "Corrected Layout to be responsive"}
						]}
					/>
					<ChangelogLine
						date="July 9, 2023"
						lines={[
							{type: "improvement", text: "Added an international mode for the Personal Knowledge Citation"},
							{type: "improvement", text: "Refreshed design of the changelog"},
							{type: "improvement", text: "Refreshed design of the site (Used the Carbon Design Language)"}
						]}
					/>
					<ChangelogLine
						date="April 27, 2023"
						lines={[
							{type: "improvement", text: "Default collection name changes for the civil record according to the type of record selected as long as it is still the default collection name"},
							{type: "bug", text: "Type for Death Civil Record indicated 'confirmation' instead of 'death'"},
						]}
					/>
					<ChangelogLine
						date="April 14, 2023"
						lines={[
							{type: "change", text: "Split the Basic Citation Builder and the Advanced Citation Builder into two separate pages and URLs"},
							{type: "new", text: "Added a Soundex Converter"},
							{type: "new", text: "Added an Updates and FAQ page"}
						]}
					/>
				</div>
			</section>
		</div>
	</main>
</Sidebar>