<script lang="ts">
  export let href: string;
</script>

<a
  {href}
  class="no-underline text-black font-semibold hover:underline active:underline transition-all duration-200"
>
  <slot />
</a>
