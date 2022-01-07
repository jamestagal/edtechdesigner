<script>
  export let title, hero;
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
        class="px-8 py-12 max-w-md mx-auto sm:max-w-xl lg:px-12 lg:py-24 lg:max-w-full xl:mr-0 2xl:col-span-2"
      >
        <div class="xl:max-w-xl">
          <img
            class="mt-6 rounded-lg shadow-xl sm:mt-8 sm:h-64 sm:w-full sm:object-cover object-center lg:hidden"
            src="assets/pages/ben-profile-pic.jpg"
            alt="Ben workcationing in the capital"
          />
          <h1
            class="mt-6 text-2xl font-bold text-gray-900 sm:mt-8 sm:text-4xl lg:text-3xl xl:text-4xl"
          >
          {hero.pre}<span class="accent-b">{hero.accent}</span>
            <br class="hidden lg:inline" />
            {hero.post}
          </h1>
          <p class="mt-2 text-gray-600 sm:mt-4 sm:text-xl">
            I design and develop educational programs in the LLND (Language Literacy, Numeracy and Digital) department at the Canberra Institute of Technology (CIT). I have taught English as a Second Language (ESL) and now EAL (English as an Additional Language) in the AMEP program both at the CIT and AMES in Victoria for over a decade. I have worked as an education designer at CIT in a team, leading the Innovative Learning Resources project as part of CIT’s Strategic Compass 2020 initiative. <br><br> My passion for language teaching, eLearning and instructional design has enabled me to develop innovative online courses and resources for a range of education projects with a focus on consistent, functional and bite-size learning design to facilitate learner engagement and rich learning experiences.
          </p>
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
          src="assets/pages/ben-profile-pic.jpg"
          alt="Woman workcationing on the beach"
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
    class="pl-2 md:pl-6 lg:pl-10 xl:pl-16 w-screen-30 sm:w-screen-40 md:w-screen-60 lg:w-screen-70 xl:w-screen-80 absolute"
    style="top: 40%"
  >
    <h2 class="header text-xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl">
      {hero.pre}<span class="accent-b">{hero.accent}</span><br />{hero.post}
    </h2>
    <h3 class="tag text-xl sm:text-2xl md:text-4xl">{hero.tagline}</h3>
  </div>
  <div />
  <div>
    <img
      class="w-full object-cover object-bottom h-screen-40 sm:h-screen-60 md:h-screen-70 lg:h-screen-80 xl:h-screen-90"
      src="assets/pages/{image.src}"
      alt={image.alt}
    />
    <span class="text-meta"
      >{@html image.citation.replaceAll(
        "<a ",
        "<a target='blank' rel='noopener noreferrer'"
      )}</span
    >
  </div>
</div>
-->

<!-- About section 
<div id="about" class="relative">
  <div class="w-full pt-10">
    <img
      class="w-full object-center object-cover h-screen-80 lg:h-screen-90"
      style="filter: brightness(60%)"
      src="assets/pages/{splash.src}"
      alt={splash.alt}
    />
  </div>
  <div
    class="absolute ml-2 md:ml-12 xl:mt-6 bg-black bg-opacity-50 w-screen-45 sm:w-screen-70 xl:w-screen-80 h-screen-70"
    style="top: 14%; overflow-y: auto;"
  >
    <div class="w-full text-lg px-6 pt-10">
      <h2 class="accent text-white text-4xl">{title}</h2>
    </div>
    <p class="text-white text-md sm:text-lg xl:text-xl px-6 py-6">
      {@html articleBody}
    </p>
  </div>
</div>
<div class="text-meta relative block">
  {@html splash.citation.replaceAll(
    "<a ",
    "<a target='blank' rel='noopener noreferrer'"
  )}
</div>
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