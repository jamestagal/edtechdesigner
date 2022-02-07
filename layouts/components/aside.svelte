<script>
  import Search from "../components/search.svelte";
  import Social from "../components/social.svelte";

  export let catg, tag, allPosts, socialLinks, catgPosts, tagsPosts;
  
  let current = false;
 
  
</script>

<aside class="w-full">
  <div class="pl-0 pl-lg-4">
    <!-- Search -->
    <Search {allPosts} />

    <!-- Social -->
    <Social {socialLinks} />

    <!-- categories -->
    <div class="row">
      <h4 class="header mb-1"><span>Categories</span></h4>
      <ul class="text-aside mb-4">
        {#each Object(catgPosts) as {page, name, length}}
          <li class="flex{catg == name ? ' active' : ''} rounded items-center mt-3 mr-3">
            <div class="customStyle border border-y-black border-l-black" class:selected={current}>
            <a on:click={() => current = true} href="catgs/{page}">{name}</a></div>
            <div style="display: flex; align-items: center; font-size: 0.8em; background-color: var(--surface); color: white; border-radius: 0px 0.25em 0.25em 0px; padding: 0px 0.5em; align-self: stretch;">{length}</div>
          </li>
        {/each}
      </ul>
    </div>

    <!-- tags -->
    <div class="row">
      <h4 class="header mb-1 w-full flex">Tags</h4>
      <ul class="text-aside mb-4">
        {#each Object(tagsPosts) as {page, name, length}}
          <li class="flex{tag == name ? ' active' : ''} rounded items-center mt-3 mr-3">
            <div class="customStyle border border-inherit border-y-black border-l-black">
            <a on:click href="tags/{page}">{name}</a></div>
            <div style="display: flex; align-items: center; font-size: 0.8em; background-color: var(--surface); color: white; border-radius: 0px 0.25em 0.25em 0px; padding: 0px 0.5em; align-self: stretch;">{length}</div>
          </li>
        {/each}
      </ul>
    </div>
  </div>
</aside>
<style>
  a:active {
    color: #F1F5F9;
  }
  .active {
    color: var(--accent);
  }
  .customStyle {
    padding: 0px 0.5em;
    border-radius: 0.25em 0px 0px 0.25em;
  }
  .selected {
    background: var(--accent);
    color: #F1F5F9;
  }
</style>