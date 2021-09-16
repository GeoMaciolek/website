<script lang="ts">
  let clazz = "";
  export { clazz as class };
  import { page } from "$app/stores";
  import type { ChangelogEntry } from "../../types/changelog-entry.type";
  import { stringToBeautifiedFragment } from "../../utils/helpers";
  import ChangelogDate from "./changelog-date.svelte";

  export let entry: ChangelogEntry;
  export let isAnEntryAlone = $page.path.split("/").length === 3;
  const { date, title, content, image, alt } = entry;
  const formattedDate = new Date(Date.parse(date)).toLocaleDateString(
    undefined,
    {
      year: "numeric",
      month: "long",
      day: "numeric",
    }
  );
</script>

<style type="text/postcss">
  .content-docs :global(h2) {
    @apply mt-12 mb-4 md:mt-16 !important;
  }

  .content-docs :global(h3) {
    @apply mt-12 mb-6 md:mt-16 md:mb-8 !important;
  }

  .content-docs :global(li) {
    @apply mt-0 mb-6 md:mb-4;
  }

  .entry {
    max-width: 800px;
    @apply mx-auto;
  }

  .entry h2 {
    @apply text-h3 !important;
  }
</style>

<div class="flex flex-col md:flex-row {clazz}" class:entry={isAnEntryAlone}>
  {#if !isAnEntryAlone}
    <ChangelogDate date={formattedDate} />
  {/if}
  <div class="{!isAnEntryAlone ? 'w-full md:w-8/12' : ''} content-docs">
    <img
      src="/images/changelog/{image}"
      class="rounded-3xl"
      alt={alt + "Test"}
    />
    {#if isAnEntryAlone}
      <p class="mt-xx-small -mb-9">{formattedDate}</p>
    {/if}
    <h2>
      {#if isAnEntryAlone}
        {title}
      {:else}
        <a
          href="/changelog/{stringToBeautifiedFragment(title)}"
          class="no-underline text-black hover:underline active:underline transition-all duration-200"
        >
          {title}
        </a>
      {/if}
    </h2>
    {@html content}
  </div>
</div>
