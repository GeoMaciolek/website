<script lang="ts">
  export let date: string;
</script>

<div class="w-full md:w-4/12">
  <p class="mb-xx-small h3 text-black font-semibold">
    {new Date(Date.parse(date)).toLocaleDateString(undefined, {
      year: "numeric",
      month: "long",
      day: "numeric",
    })}
  </p>
</div>
