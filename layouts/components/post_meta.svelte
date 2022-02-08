<script>
  import { get_description } from "../scripts/get_description.svelte";
  export let post, catgPosts, tagsPosts, pm;

  let path = post.path;
  let author_url = post.author_url ?? post.fields.author.url;
  let author_name = post.author_name ?? post.fields.author.name;
  let dateCreated = post.dateCreated ?? post.fields.dateCreated;
  let dateModified = post.dateModified ?? post.fields.dateModified;
  let tags = post.tags ?? post.fields.tags;
  let catgs = post.catgs ?? post.fields.categories;
  let cardBody = pm.description
    ? get_description(post.fields.articleBody, 170)
    : "";
</script>

{#if pm.author}
  <li class="mx-0 -mt-1 text-meta inline-flex">
    <i class="las la-user-astronaut{pm.feature ? ' feature' : ' standard'}" />
  </li>
<li class="mr-2 my-0 inline-flex">
  <a href={author_url}>{author_name}</a>
</li>
{/if}
{#if pm.date_created}
  <li class="mr-2 my-0 inline-flex">
    {dateCreated}
  </li>
{/if}
{#if pm.date_modified}
  <li class="mr-2 my-0 inline-flex">
    Updated: {dateModified}
  </li>
{/if}
{#if pm.catg_tags}
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
{#if pm.description}
  <p class="text-base">
    {@html cardBody}
  </p>
{/if}
{#if pm.continue}
  <article class="border-0">
    <div class="mb-4">
      <a href={path} class="btn-outline hover:white">Read more</a>
    </div>
  </article>
{/if}

<style>
  .standard {
    font-size: 1rem;
    line-height: 1.5rem;
    margin-top: 3px;
  }
  .feature {
    color: rgba(255, 255, 255, 0.9);
    margin-top: 3px;
  }
  @media (max-width: 767px) {
    .feature {
      font-size: 1.125rem;
      line-height: 1.75rem;
    }
  }
  @media (min-width: 768px) {
    .feature {
      font-size: 1.25rem;
      line-height: 1.75rem;
    }
  }
  @media (min-width: 1024px) {
    .feature {
      font-size: 1.5rem;
      line-height: 2rem;
    }
  }
</style>
