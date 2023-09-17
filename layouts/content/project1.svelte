<script>
  import { fade } from "svelte/transition";
  import SlidesNav from "../components/slides_nav.svelte";
  export let title, description, h5p, order, content;
</script>

<head>
  <script
    src="https://edtechdesigner.h5p.com/js/h5p-resizer.js"
    charset="UTF-8"
  >
  </script>
</head>
<!-- <Sidenav /> -->
<section class="section flex items-center py-6 sm:py-12">
  <div class="w-0 md:w-1/12 xl:w-2/12" />
  <div class="w-full md:w-10/12 xl:w-8/12 px-2 md:px-0">
    <div class="row flex center; flex-wrap">
      <div class="relative mb-8 w-full">
        <h2>{title}</h2>
        <p>
          {description}
        </p>
        <SlidesNav />
        <a class="control" href="slide/{Number(order) - 1}">Previous</a>
        <a class="control" href="slide/{Number(order) + 1}">Next</a>
        {#key content}
          <div id="slide" transition:fade>
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
            <a id="exit" href=".">Exit</a>
          </div>
        {/key}
      </div>
    </div>
  </div>
</section>

<style>
  .control {
    display: flex;
    position: absolute;
    margin: 20px;
  }
  .control:first-of-type {
    left: 0;
  }
  .control:last-of-type {
    right: 0;
  }
</style>