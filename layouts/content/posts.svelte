<script>
  // Aside component for search, categories, and tags
  import Aside from "../components/aside.svelte";
  import PostMeta from "../components/post_meta.svelte";

  // Values passed in from "html.svelte"
  export let idxContent, allPosts, catgPosts, tagsPosts;

  // Content field Values passed in via layout content {...content.fields}
  export let articleBody, title, author;
  export let dateCreated, dateModified, categories, tags, h5p, youtube;

  // Post Meta configuration values
  const pm = {
    author: true,
    date_modified: true,
    date_created: true,
    description: false,
    catg_tags: true,
    continue: false,
  };

  let socialLinks = idxContent.socialLinks;
  let post = {
    author_url: author.url,
    author_name: author.name,
    dateCreated: dateCreated,
    dateModified: dateModified,
    tags: tags,
    catgs: categories,
  };
</script>

<head>
  <script
 src="https://edtechdesigner.h5p.com/js/h5p-resizer.js" charset="UTF-8">
  </script>
</head>

<section
  class="section flex flex-wrap items-center justify-between py-6 sm:py-12"
>
  <div class="w-0 md:w-1/12 xl:w-2/12" />
  <div class="w-full md:w-10/12 xl:w-8/12 px-2 md:px-0">
    <div class="row flex flex-wrap">
<!--       {#if !youtube || !h5p }
      <div class="relative mb-8 w-full">
        <img
          class="rounded-lg overflow-hidden w-full h-screen-60 object-cover object-center"
          src="media/posts/{image.src}"
          alt={image.alt}
        />
        <cite class="text-meta"
          >{@html image.citation.replaceAll(
            "<a ",
            "<a target='blank' rel='noopener' "
          )}</cite
        >
      </div>
      {/if} -->
      <div class="w-full md:w-9/12 mb-5 sm:mb-0 px-0 md:pr-10" role="article">
        <h1 class="header mb-2">{title}</h1>
        <div class="text-meta flex flex-wrap" role="complementary">
          <PostMeta {post} {catgPosts} {tagsPosts} {pm} />
        </div>
      <p class="mt-6" role="main">
          {@html articleBody}
        </p>
      </div>
        <!-- Aside  -->
        <div class="w-full order-last md:order-none md:w-3/12 mb-5 mb-lg-0 px-0">
          <Aside {allPosts} {catgPosts} {tagsPosts} {socialLinks} />
        </div>
        {#if youtube}
        <div class="youtube relative mb-8 w-full">
          <iframe 
            style="position:absolute;top:0;left:0;width:100%;height:100%;"
            title="YouTube video player"
            frameborder="0"
            allowfullscreen="allowfullscreen"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            src={youtube.src}
          />
        </div>
      {/if}
          {#if h5p}
            <div class="relative mb-8 w-full">
              <iframe 
                class="w-full h-full" 
                title={title}
                width="1088"
                height="637"
                frameborder="0"
                allowfullscreen="allowfullscreen"
                allow="geolocation *; microphone *; camera *; midi *; encrypted-media *"
                src={h5p.src}
              />
            </div>
          {/if}
    </div>
  </div>
  <div class="w-0 md:w-1/12 xl:w-2/12" />
</section>
<style>
.youtube {
  position:relative;
  padding-top:56.25%;
}
</style>