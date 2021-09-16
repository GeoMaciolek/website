<script lang="ts" context="module">
  export async function load({ session }) {
    const changelogEntries = session.changelogEntries;
    return { props: { changelogEntries } };
  }
</script>

<script lang="ts">
  import type { ChangelogEntry as ChangelogEntryType } from "../../types/changelog-entry.type";

  import OpenGraph from "../../components/open-graph.svelte";
  import NewsletterSignup from "../../components/blog/newsletter-signup.svelte";
  import "../../assets/markdown-commons.scss";
  import Modal from "../../components/modal.svelte";
  import TwitterFollowButton from "../../components/twitter-follow-button.svelte";
  import ChangelogEntry from "../../components/changelog/changelog-entry.svelte";

  export let changelogEntries: ChangelogEntryType[];

  let isNewsLetterFormShown: boolean = false;

  const handleClose = () => {
    isNewsLetterFormShown = false;
  };
</script>

<OpenGraph
  data={{
    description: "New features and improvements to Gitpod.",
    title: "Changelog",
    type: "website",
  }}
/>

<div class="flex">
  <div class="hidden w-4/12 md:block" />
  <header class="w-full mb-x-large md:w-8/12 md:mb-xx-large">
    <h1 class="mt-x-large mb-macro md:mt-xx-large">Changelog</h1>
    <p>Gitpod product improvements and updates</p>
    <p class="mt-micro">
      <TwitterFollowButton trackingContext="changelog" class="btn-primary" />
      <button
        class="btn-secondary"
        on:click={() => (isNewsLetterFormShown = true)}
      >
        Signup for the Newsletter
      </button>
    </p>
  </header>
</div>

<div class="flex flex-col space-y-x-large md:space-y-xx-large">
  {#each changelogEntries as entry}
    <ChangelogEntry {entry} />
    <div class="border-b border-gray-300" />
  {/each}
</div>
<div class="flex py-large md:py-x-large">
  <div class="hidden w-4/12 md:block" />
  <div class="w-full md:w-8/12">
    <p>
      For older updates, please visit <a href="/docs/changelog"
        >the previous changelog.</a
      >
    </p>
  </div>
</div>

<Modal isOpen={isNewsLetterFormShown} on:close={handleClose}>
  <NewsletterSignup />
</Modal>
