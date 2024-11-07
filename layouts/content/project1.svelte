<script>
  import { fade } from "svelte/transition";
  import SlidesNav from "../components/slides_nav.svelte";
  import { count } from "../scripts/stores.svelte";
  export let title, description, h5p, order, content;
  let totalSlides;
  let currentSlide;

  $: {
    totalSlides = order.length;
    currentSlide = $count;
    console.log('Current slide:', currentSlide, 'Total slides:', totalSlides); // Debug log
  }

  $: isLastSlide = currentSlide === totalSlides;
  $: isFirstSlide = currentSlide === 1;

  function goToSlide(n) {
    const newSlide = Math.max(1, Math.min(n, totalSlides));
    count.set(newSlide);
    console.log('Navigating to slide:', newSlide); // Debug log
  }
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
  <div class="md:w-10/12 xl:w-8/12 px-2 md:px-0">
    <div class="row flex center; flex-wrap">
      <div class="relative mb-8 w-full">
        <h2>{title}</h2>
        <p>
          {description}
        </p>
        <div class="z-10 flex flex-none py-3 px-4 mobile-sm:justify-between">
          <div
            class="flex items-center mr-10 flex-1 mobile-sm:hidden inherited-styles-for-exported-element"
          >
            <div class="w-7">
              <svg
                aria-hidden="true"
                focusable="false"
                data-prefix="fas"
                data-icon="house"
                class="svg-inline--fa fa-house mx-auto block text-base leading-4 text-indigo-500 transition-transform duration-300 scale-100"
                role="img"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 576 512"
              >
                <path
                  fill="currentColor"
                  d="M575.8 255.5c0 18-15 32.1-32 32.1h-32l.7 160.2c0 2.7-.2 5.4-.5 8.1V472c0 22.1-17.9 40-40 40H456c-1.1 0-2.2 0-3.3-.1c-1.4 .1-2.8 .1-4.2 .1H416 392c-22.1 0-40-17.9-40-40V448 384c0-17.7-14.3-32-32-32H256c-17.7 0-32 14.3-32 32v64 24c0 22.1-17.9 40-40 40H160 128.1c-1.5 0-3-.1-4.5-.2c-1.2 .1-2.4 .2-3.6 .2H104c-22.1 0-40-17.9-40-40V360c0-.9 0-1.9 .1-2.8V287.6H32c-18 0-32-14-32-32.1c0-9 3-17 10-24L266.4 8c7-7 15-8 22-8s15 2 21 7L564.8 231.5c8 7 12 15 11 24z"
                />
              </svg>
            </div>
            <div class="relative flex flex-1 items-center">
              <div class="absolute w-full bg-blueGray-300 h-px">
                <div
                  class="absolute w-full origin-left bg-indigo-500 transition-transform duration-300 h-px"
                  style="transform: scaleX({($count - 1) / (totalSlides - 1)});"
                />
              </div>
              <div class="absolute flex w-full items-center bg-blend-multiply">
                {#each Array(totalSlides) as _, i (i)}
                <div
                on:click={() => goToSlide(i + 1)}
                class="absolute cursor-pointer"
                class:active={currentSlide === i + 1}
                style="left: calc({100 * i / (totalSlides - 1)}% - 0.25rem);"
              >
                  <div
                    class="rounded-full bg-white transition-all scale-150 absolute"
                    style="width: 8px; height: 8px; margin-top: -4px; margin-left: -4px;"
                  />
                  <div
                    class="rounded-full transition-colors bg-blueGray-300 absolute"
                    style="width: 8px; height: 8px; margin-top: -4px; margin-left: -4px;"
                  />
                </div>
                {/each}
              </div>
            </div>
          </div>
          <a
             on:click={() => goToSlide(currentSlide - 1)}
              href="h5p/example/slide/{currentSlide - 1}"
            class="flex items-center justify-center rounded-lg border border-slate-200 bg-transparent p-3"
            class:opacity-50={isFirstSlide}
            class:cursor-not-allowed={isFirstSlide}
            aria-label="back to previous step"
            tabindex="0"
            ><svg
              stroke="currentColor"
              fill="currentColor"
              stroke-width="0"
              viewBox="0 0 24 24"
              class="h-4 w-4 text-slate-800 transition-opacity opacity-50"
              height="1em"
              width="1em"
              xmlns="http://www.w3.org/2000/svg"
              ><g
                ><path fill="none" d="M0 0h24v24H0z" /><path
                  d="M7.828 11H20v2H7.828l5.364 5.364-1.414 1.414L4 12l7.778-7.778 1.414 1.414z"
                /></g
              ></svg
            ></a
          >

          <a
             on:click={() => goToSlide(currentSlide + 1)}
            href="h5p/example/slide/{currentSlide + 1}"
            class="flex h-[42px] select-none items-center rounded-lg px-3 leading-4 transition-[width] duration-300 bg-gradient-to-b from-indigo-500 to-indigo-600 w-[132px] cursor-pointer hover:from-indigo-600 hover:to-indigo-700 ml-4"
            class:opacity-50={isLastSlide}
            class:cursor-not-allowed={isLastSlide}
            class:hover:from-indigo-600={!isLastSlide}
            class:hover:to-indigo-700={!isLastSlide}
            disabled={isLastSlide}
            tabindex="0"
            aria-label={isLastSlide ? "Last slide" : "Go to next step"}
          >
            <svg
              stroke="currentColor"
              fill="currentColor"
              stroke-width="0"
              viewBox="0 0 24 24"
              class="mr-2 text-indigo-200"
              height="16px"
              width="16px"
              xmlns="http://www.w3.org/2000/svg"
              ><g
                ><path fill="none" d="M0 0h24v24H0z" /><path
                  d="M16.172 11l-5.364-5.364 1.414-1.414L20 12l-7.778 7.778-1.414-1.414L16.172 13H4v-2z"
                  class=""
                /></g
              ></svg
            ><span
              class="whitespace-nowrap text-sm font-semibold text-white transition-opacity duration-300 opacity-100"
              >{isLastSlide ? "Last" : "Next"}</span
            ></a
          >
        </div>
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
          </div>
        {/key}
      </div>
    </div>
  </div>
</section>

<style>
  * {
    box-sizing: border-box;
  }

  *,
  ::after,
  ::before {
    border-style: solid;
    border-width: 0;
  }
  .active {
    background-color: rgb(99 102 241 / 1);
  }
  .svg-inline--fa {
    height: 1em;
    overflow: visible;
    vertical-align: -0.125em;
  }

  .absolute {
    position: absolute;
  }

  .relative {
    position: relative;
  }

  .mx-auto {
    margin-left: auto;
    margin-right: auto;
  }

  .mr-10 {
    margin-right: 2.5rem;
  }

  .block {
    display: block;
  }

  .flex {
    display: flex;
  }

  .h-px {
    height: 1px;
  }

  .w-full {
    width: 100%;
  }

  .w-7 {
    width: 1.75rem;
  }

  .flex-1 {
    flex: 1 1 0;
  }

  .origin-left {
    transform-origin: left center;
  }

  .scale-100 {
    transform: matrix(1, 0, 0, 1, 0, 0);
  }

  .scale-150 {
    transform: matrix(1.5, 0, 0, 1.5, 0, 0);
  }

  .cursor-pointer {
    cursor: pointer;
  }

  .items-center {
    align-items: center;
  }

  .rounded-full {
    border-radius: 9999px;
  }

  .bg-white {
    background-color: rgb(255 255 255/1);
  }

  .bg-indigo-500 {
    background-color: rgb(99 102 241/1);
  }

  .bg-blueGray-300 {
    background-color: rgb(203 213 225/1);
  }

  .inherited-styles-for-exported-element {
    font-family: "Public Sans", ui-sans-serif, system-ui, -apple-system,
      BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial,
      "Noto Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji",
      "Segoe UI Symbol", "Noto Color Emoji";
  }

  .text-base {
    font-size: 1rem;
  }

  .leading-4 {
    line-height: 1rem;
  }

  .text-indigo-500 {
    color: rgb(99 102 241/1);
  }

  .bg-blend-multiply {
    background-blend-mode: multiply;
  }

  .transition-all {
    transition: all 0.15s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .transition-colors {
    transition-duration: 0.15s;
    transition-property: color, background-color, border-color,
      text-decoration-color, fill, stroke;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  }

  .transition-transform {
    transition: transform cubic-bezier(0.4, 0, 0.2, 1);
  }

  .transition-opacity {
    transition-property: opacity;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 0.15s;
  }
  .opacity-50 {
    opacity: 0.5;
  }
  .text-slate-800 {
    --tw-text-opacity: 1;
    color: rgb(30 41 59 / var(--tw-text-opacity));
  }
  .p-3 {
    padding: 0.75rem;
  }
  .bg-transparent {
    background-color: transparent;
  }
  .border-slate-200 {
    --tw-border-opacity: 1;
    border-color: rgb(226 232 240 / var(--tw-border-opacity));
  }
  .border {
    border-width: 1px;
  }
  .duration-300 {
    transition-duration: 0.3s;
  }

  @media (max-width: 320px) {
    .mobile-sm\:hidden {
      display: none;
    }
  }

  svg:not(:host).svg-inline--fa,
  svg:not(:root).svg-inline--fa {
    box-sizing: content-box;
    overflow: visible;
  }
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
