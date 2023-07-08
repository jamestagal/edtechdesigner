<script>
    import Hoverable from "../scripts/hoverable.svelte";
  export let title, hero, articleBody;

  function scrollDown() {
    window.scrollTo({
      top: 900,
      left: 0,
      behavior: "smooth",
    });
  }
</script>
<head>
  <script
 src="https://edtechdesigner.h5p.com/js/h5p-resizer.js" charset="UTF-8">
  </script>
</head>
<!-- Test Hero section-->

  <body class="bg-gray-300">
    <div class="bg-gray-100 grid lg:grid-cols-2 2xl:grid-cols-5">
      <div
        class="px-8 py-12 max-w-md mx-auto sm:max-w-xl lg:px-12  lg:max-w-full xl:mr-0 2xl:col-span-2"
      >
        <div class="xl:max-w-xl">
          <img
            class="mt-6 rounded-lg shadow-xl sm:mt-8 sm:h-64 sm:w-full sm:object-cover object-center lg:hidden"
            src="media/pages/ben-profile-pic.webp"
            alt="Ben workcationing in the capital"
          />
          <div class="container">
            <div class="image">
              <img src="media/pages/h5p-ambassador-2023.png" alt="H5P Embassador Benjamin Waller">
            </div>
          <h1
            class="text mt-6 text-2xl font-bold text-gray-900 sm:mt-6 sm:text-3xl lg:text-3xl xl:text-3xl"
          >
          {hero.pre}<span class="accent-b">{hero.accent}</span>
            <br class="hidden lg:inline" />
            {hero.post}
          </h1>
        </div>
          <p class="mt-2 text-gray-600 sm:mt-4 sm:text-xl">
           {@html articleBody}
          </p>
          <button
          type="button"
          on:click={scrollDown}
          class="absolute bottom-0 sm:bottom-10 md:bottom-20"
          style="left: 25%; transform: translate(-50%);"
        >
          <Hoverable let:hovering>
            <span class="inline-block {hovering ? 'animate-bounce' : ''}">
              <i
                class="accent las la-chevron-circle-down text-5xl lg:text-6xl rounded-full overflow-hidden bg-clip-content opacity-80 hover:opacity-100"
              />
            </span>
          </Hoverable>
          </button>
          <!-- Button
          <div class="mt-4 sm:mt-6">
            <a
              class="inline-block px-5 py-3 rounded-lg bg-indigo-500 uppercase tracking-wider font-semibold text-sm text-white shadow-lg sm:text-base"
              href="https://www.benjaminjameswaller.com/"
            >
              See my person blog
            </a>
          </div>
          -->
        </div>
      </div>
      <div class="hidden relative lg:block 2xl:col-span-3">
        <img
          class="absolute inset-0 w-full h-full object-cover object-center"
          src="media/pages/ben-profile-pic.webp"
          alt="Benjamin Waller in a field"
        />
      </div>
    </div>
  </body>

<!-- NEW Hero section
<div id="hero" class="container mx-auto relative">
  <h2 class="header text-xl sm:text-3xl md:text-4xl lg:text-5xl">
    {hero.pre}<span class="accent-b">{hero.accent}</span><br />{hero.post}
  </h2>
  <iframe 
  class="w-full h-full" 
  title={title}
  width="1088"
  height="637"
  frameborder="0"
  allowfullscreen="allowfullscreen"
  allow="geolocation *; microphone *; camera *; midi *; encrypted-media *"
  src="https://edtechdesigner.h5p.com/content/1291111834028671999/embed"
/>
</div>
-->
<!-- Original Hero section
<div id="hero" class="w-full grid grid-cols-2 relative">
  <div
    class="pl-2 md:pl-6 lg:pl-10 xl:pl-16 w-screen-30 sm:w-screen-40 md:w-screen-50 lg:w-screen-60 xl:w-screen-80 absolute bottom-10 sm:bottom-1/4"
  >
    <h2 class="header text-xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl">
      {hero.pre}<span class="accent-b">{hero.accent}</span><br />{hero.post}
    </h2>
    <h3 class="tag text-base sm:text-xl md:text-2xl lg:text-3xl xl:text-4xl">
      {hero.tagline}
    </h3>
  </div>
  <div />
  <div>
    <img
      class="w-full object-cover object-bottom h-screen-40 sm:h-screen-60 md:h-screen-70 lg:h-screen-80 xl:h-screen-90"
      src="media/pages/{image.src}"
      alt={image.alt}
    />
    <cite class="text-meta"
      >{@html image.citation.replaceAll(
        "<a ",
        "<a target='blank' rel='noopener' "
      )}</cite
    >
  </div>
  <Hoverable let:hovering>
  <button
    type="button"
    on:click={scrollDown}
    class="absolute bottom-0 sm:bottom-10 md:bottom-20"
    style="left: 25%; transform: translate(-50%);"
  >
      <span class="inline-block {hovering ? 'animate-bounce' : ''}">
        <i
          class="accent las la-chevron-circle-down text-5xl lg:text-6xl rounded-full overflow-hidden bg-clip-content opacity-80 hover:opacity-100"
        />
      </span>
  </button>
  </Hoverable>
</div>
-->

<!-- About section 
<div id="about" class="relative">
  <div class="w-full pt-16">
    <img
      class="w-full object-center object-cover h-screen-80 lg:h-screen-90"
      style="filter: brightness(60%)"
      src="media/pages/{splash.src}"
      alt={splash.alt}
    />
  </div>
  <div
    class="absolute ml-2 md:ml-12 xl:mt-6 bg-black bg-opacity-50 w-screen-45 sm:w-screen-70 lg:w-screen-80 h-screen-70"
    style="top: 14%; overflow-y: auto;"
  >
    <div class="w-full text-lg px-6 pt-10">
      <h2 class="accent text-white text-4xl">{title}</h2>
    </div>
    <p class="text-white text-md sm:text-lg lg:text-xl 2xl:text-2xl px-6 py-6">
      {@html articleBody}
    </p>
  </div>
</div>
<cite class="text-meta relative block">
  {@html splash.citation.replaceAll("<a ", "<a target='blank' rel='noopener' ")}
</cite>
-->
<!-- About section - Employment Timeline -->
<div id="timeline" class="container mx-auto relative pt-10">
  <iframe 
  class="w-full h-full" 
  title={title}
  width="1088"
  height="637"
  frameborder="0"
  allowfullscreen="allowfullscreen"
  allow="geolocation *; microphone *; camera *; midi *; encrypted-media *"
  src="https://edtechdesigner.h5p.com/content/1291111834693905529/embed"
/>
</div>

<style>
  .container {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  img {
    max-width: 100%
  }
  .image {
    flex-basis: 70%;
    order: 2;
  }
  .text {
    text-wrap: balance;
  }
</style>