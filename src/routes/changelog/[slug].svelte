<script lang="ts" context="module">
  import ChangelogEntry from "../../components/changelog/changelog-entry.svelte";
  import { stringToBeautifiedFragment } from "../../utils/helpers";
  import type { ChangelogEntry as ChangelogEntryType } from "../../types/changelog-entry.type";

  export async function load({ page, session }) {
    const changelogEntry: ChangelogEntryType = session.changelogEntries.find(
      (entry: ChangelogEntryType) =>
        stringToBeautifiedFragment(entry.title) === page.params.slug
    );
    return { props: { changelogEntry } };
  }
</script>

<script lang="ts">
  export let changelogEntry: ChangelogEntryType;
</script>

<ChangelogEntry entry={changelogEntry} class="py-20" />
