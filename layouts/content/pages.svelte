<script>
  export let idxContent,
    allLayouts,
    allPosts,
    content,
    catgPosts,
    tagsPosts,
    baseurl;

  const getComponent = function () {
    try {
      return allLayouts[
        "layouts_components_page_" + content.path.split("/")[1] + "_svelte"
      ];
    } catch (e) {
      return false;
    }
  };
</script>

{#if content.fields.enabled}
  <div class="w-full py-6 sm:py-12">
    <svelte:component
      this={getComponent()}
      {...content.fields}
      {idxContent}
      {content}
      {allPosts}
      {catgPosts}
      {tagsPosts}
      {baseurl}
    />
  </div>
{/if}
