<script lang="ts">
  import ChangelogLink from "./changelog-link.svelte";

  export let date: string;
  export let href: string;
</script>

<div class="w-full md:w-4/12">
  <ChangelogLink {href}>
    <p class="mb-xx-small h3 text-black">
      {new Date(Date.parse(date)).toLocaleDateString(undefined, {
        year: "numeric",
        month: "long",
        day: "numeric",
      })}
    </p>
  </ChangelogLink>
</div>
