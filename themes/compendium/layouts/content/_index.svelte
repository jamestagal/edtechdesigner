<script>
  import Featured from "../components/featured.svelte";
  import MainSection from "../components/main.svelte";

  // Variables passed in from "html.svelte"
  // * content: values for keys in "index.json"
  // * allPosts: values for keys in all posts
  // * theme: values passed in from layout content {...content.fields}
  export let allPosts, content, theme, catgPosts, tagsPosts, baseurl;

  $: currentPage = content.pager ? content.pager : 1;
  let featuredPage = theme.featuredPage;
  let postsPerPage = 4;
  let allFeatures = allPosts.filter((content) => content.fields?.featured);
  let totalPosts = allPosts.length;
  let totalPages = Math.ceil(totalPosts / postsPerPage);
  $: postRangeHigh = currentPage * postsPerPage;
  $: postRangeLow = postRangeHigh - postsPerPage;
</script>

<section class="flex flex-wrap items-center justify-between pb-11">
  <!-- ------------------------------------------------------- -->
  <!-- Loop through all the posts and process featured only    -->
  <!-- ------------------------------------------------------- -->
  {#if featuredPage == "Bleed" && currentPage <= 1}
    <div class="w-full row -mt-16">
      <Featured {allFeatures} {featuredPage} {catgPosts} {tagsPosts} />
    </div>
  {/if}

  <div class="w-0 md:w-1/12 xl:w-2/12" />
  <div class="w-full md:w-10/12 xl:w-8/12 px-2 md:px-0">
    {#if featuredPage == "Frame" && currentPage <= 1}
      <div class="w-full row mt-6 sm:mt-16">
        <Featured {allFeatures} {featuredPage} {catgPosts} {tagsPosts} />
      </div>
    {/if}

    <!-- ------------------------------------------------------- -->
    <!-- Loop through all the posts and generate cards and aside -->
    <!-- ------------------------------------------------------- -->
    <div class="w-full">
      <MainSection
        {allPosts}
        {catgPosts}
        {tagsPosts}
        {content}
        {postRangeHigh}
        {postRangeLow}
        {currentPage}
        {totalPages}
        {baseurl}
      />
    </div>
  </div>
  <div class="w-0 md:w-1/12 xl:w-2/12" />
</section>
