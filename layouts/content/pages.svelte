<script>
  export let idxContent,
    allLayouts,
    allPosts,
    content,
    enabled,
    title,
    image,
    hero,
    splash,
    articleBody,
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

{#if enabled}
  <div class="w-full py-6 sm:py-12">
    <svelte:component
      this={getComponent()}
      {idxContent}
      {content}
      {allPosts}
      {title}
      {image}
      {hero}
      {splash}
      {articleBody}
      {catgPosts}
      {tagsPosts}
      {baseurl}
    />
  </div>
{/if}
