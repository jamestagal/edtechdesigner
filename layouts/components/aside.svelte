<script>
  import { onMount } from "svelte";
  import Search from "../components/search.svelte";
  import Social from "../components/social.svelte";

  export let allPosts, socialLinks, tagsList, catgList;
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
        {#each catgList as catg, i}
          <li class="flex rounded items-center mt-3 mr-3">
            <div style="padding: 0px 0.5em; border: 1px solid black; border-radius: 0.25em 0px 0px 0.25em;">
            <a href="catgs/{i + 1}">{catg}</a></div>
            <div style="display: flex; align-items: center; font-size: 0.8em; background-color: black; color: white; border-radius: 0px 0.25em 0.25em 0px; padding: 0px 0.5em; align-self: stretch;">{catgList.length}</div>
          </li>
        {/each}
      </ul>
    </div>

    <!-- tags -->
    <div class="row">
      <h4 class="header mb-1 w-full flex">Tags</h4>
      <ul class="text-aside mb-4">
        {#each tagsList as tag, i}
          <li class="flex">
            <a href="tags/{i + 1}">{tag}</a>
          </li>
        {/each}
      </ul>
    </div>
  </div>
</aside>
