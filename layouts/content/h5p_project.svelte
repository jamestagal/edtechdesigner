<script>
  import { fade } from "svelte/transition";
  
  export let order, title, description, h5p, allContent;

  let currentPage;
  let totalPages;

  $: {
    totalPages = allContent.filter(content => 
      content.path.startsWith('h5p/example/')
    ).length;
    currentPage = Number(order);
  }
</script>

<head>
  <script
    src="https://edtechdesigner.h5p.com/js/h5p-resizer.js"
    charset="UTF-8"
  >
  </script>
</head>

<!-- Navigation Menu -->
<div class="flex pagination text-center justify-center pt-8" role="navigation">
  <!-- Previous Buttons -->
  {#if Number(order) > 1}
    <a href="h5p/example/1" class="btn-round m-0.5" aria-label="First">
      <i class="las la-angle-double-left font-black" />
    </a>
    <a
      href="h5p/example/{Number(order)-1}"
      class="btn-round m-0.5"
      aria-label="Previous">
      <i class="las la-angle-left font-black" />
    </a>
  {:else}
    <button class="btn-round-inactive m-0.5" aria-label="First">
      <i class="las la-angle-double-left font-black" />
    </button>
    <button class="btn-round-inactive m-0.5" aria-label="Previous">
      <i class="las la-angle-left font-black" />
    </button>
  {/if}

  <!-- Number Buttons -->
  {#each Array(totalPages) as _, i}
    {#if Number(order) === i + 1}
      <button class="btn-round-active m-0.5">{i + 1}</button>
    {:else}
      <a class="btn-round m-0.5" href="h5p/example/{i + 1}">{i + 1}</a>
    {/if}
  {/each}

  <!-- Next Buttons -->
  {#if Number(order) < totalPages}
    <a
      href="h5p/example/{Number(order)+1}"
      class="btn-round m-0.5"
      aria-label="Next">
      <i class="las la-angle-right font-black" />
    </a>
    <a href="h5p/example/{totalPages}" class="btn-round m-0.5" aria-label="Last">
      <i class="las la-angle-double-right font-black" />
    </a>
  {:else}
    <button class="btn-round-inactive m-0.5" aria-label="Next">
      <i class="las la-angle-right font-black" />
    </button>
    <button class="btn-round-inactive m-0.5" aria-label="Last">
      <i class="las la-angle-double-right font-black" />
    </button>
  {/if}
</div>

<!-- Main Content Section -->
<section class="section flex items-center py-6 sm:py-6">
  <div class="w-0 md:w-1/12 xl:w-2/12" />
  <div class="md:w-10/12 xl:w-8/12 px-2 md:px-0">
    <div class="row flex center; flex-wrap">
      <div class="relative mb-8 w-full">
        <h2>{title}</h2>
        <p>{description}</p>
        
        <!-- Content Display -->
        <div transition:fade>
          <iframe
            class="w-full h-full"
            {title}
            width="1088"
            height="637"
            frameborder="0"
            allowfullscreen="allowfullscreen"
            allow="geolocation *; microphone *; camera *; midi *; encrypted-media *"
            src={h5p.src}
          />
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .las {
    top: 0px;
  }
</style>