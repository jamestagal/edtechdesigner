<script>
  import { get_description } from "../scripts/get_description.svelte";
  export let post, catgPosts, tagsPosts, complete, skipbody;

  let path = post.path;
  let author_url = post.author_url ?? post.fields.author.url;
  let author_name = post.author_name ?? post.fields.author.name;
  let dateCreated = post.dateCreated ?? post.fields.dateCreated;
  let dateModified = post.dateModified ?? post.fields.dateModified;
  let tags = post.tags ?? post.fields.tags;
  let catgs = post.catgs ?? post.fields.categories;
  let cardBody = skipbody
    ? "skip"
    : get_description(post.fields.articleBody, 170);
</script>

<li class="mr-2 my-0 inline-flex">
  <a href={author_url}>{author_name}</a>
</li>
{#if complete}
  <li class="mr-2 my-0 inline-flex">
    Created: {dateCreated}
  </li>
{/if}
<li class="mr-2 my-0 inline-flex">
  Updated: {dateModified}
</li>
{#if complete}
  <br />
  <li class="mr-2 my-0 flex">
    <div style="display: flex; align-items: center; font-size: 0.8em; background-color: var(--surface); color: white; padding: 0px 0.5em; align-self: stretch; border-radius: 0.25em 0px 0px 0.25em;">
    Category</div>
    {#each catgs as catg, i}
      {#each Object(catgPosts) as { page, name }}
        {#if catg == name}
        <div class="border border-inherit border-y-black border-l-black bg-white" style="padding: 0px 0.5em; border-radius: 0px 0.25em 0.25em 0px; text-decoration: none;">
          <a href="catgs/{page}" class="ml-0.5">
            {name}{#if i < catgs.length - 1},{/if}
          </a></div>
        {/if}
      {/each}
    {/each}
  </li>
  <li class="mr-2 my-0 inline-flex">
    <div style="display: flex; align-items: center; font-size: 0.8em; background-color: var(--surface); color: white; padding: 0px 0.5em; align-self: stretch; border-radius: 0.25em 0px 0px 0.25em;">
    Tags</div>
    {#each tags as tag, i}
      {#each Object(tagsPosts) as { page, name }}
        {#if tag == name}
        <div class="border border-inherit border-y-black border-l-black bg-white" style="padding: 0px 0.5em; border-radius: 0px 0.25em 0.25em 0px; text-decoration: none;">
          <a href="tags/{page}" class="ml-0.5">
            {name}{#if i < tags.length - 1},{/if}
          </a></div>
        {/if}
      {/each}
    {/each}
  </li>
{/if}
{#if cardBody !== "skip"}
  <p class="text-base">
    {@html cardBody}
  </p>
  <article class="border-0">
    <div class="mb-4">
      <p class="mb-6" />
      <a href={path} class="btn-outline hover:white">Read more</a>
    </div>
  </article>
{/if}
