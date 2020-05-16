<style>
  .about-detail {
    border-bottom-left-radius: 200px;
    transform: translateX(90vw);
    transition: transform 1000ms cubic-bezier(0.42, 1.04, 0.48, 1.16);
  }

  .about-detail:hover {
    transform: translateX(10vw);
  }

  @media only screen and (min-width: 768px) {
    .about-detail:hover {
      transform: translateX(20vw);
    }
  }

  @media only screen and (min-width: 1024px) {
    .about-detail {
      border-bottom-left-radius: 0;
      transform: translateX(95vw);
    }
  }

  .grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-flow: dense;
    gap: 5px;
  }

  .grid-container > li {
    height: 70px;
    color: linen;
    overflow-wrap: anywhere;
    display: flex;
    align-items: center;
    position: relative;
  }

  .bg {
    background-image: url('https://images.unsplash.com/photo-1530819568329-97653eafbbfa?ixlib=rb-1.2.1&auto=format&fit=crop&w=746&q=80');
    background-size: contain;
    background-attachment: fixed;
    height: 100%;
    width: 100%;
    filter: blur(3px);
    position: absolute;
    z-index: -1;
  }

  .grid-container > li:last-child {
    grid-column: 2 / -1;
  }

  .cert-link:link,
  .cert-link:visited {
    color: #a0aec0;
    text-decoration: underline;
    transition: color 300ms ease-in;
  }

  .cert-link:hover,
  .cert-link:active {
    color: white;
  }
</style>

<script>
  import { fade, fly } from 'svelte/transition';
  import { expoOut } from 'svelte/easing';

  import ArrowRight from '../Arrow/ArrowRight.svelte';
  import ArrowLeft from '../Arrow/ArrowLeft.svelte';

  const stacks = [
    'HTML',
    'CSS',
    'JS',
    'React',
    'React Native',
    'Redux',
    'NodeJS',
    'MongoDB',
    'PostgreSQL',
    'TypeScript',
    'SASS'
  ];

  const certs = [
    { org: 'FreeCodeCamp', course: 'Full Stack' },
    { org: 'Microsoft', course: 'Artificial Intelligence' },
    { org: 'Udacity', course: 'React Nanodegree' },
    { org: 'Udemy', course: 'Advanced CSS' }
  ];

  let slideNo = 0;
  const flyIn = { x: 500, delay: 550, duration: 1500, easing: expoOut };
  const fadeOut = { duration: 500 };
  const sectionClass =
    'h-full flex flex-col justify-center pl-12 pr-10 transition-all text-sm sm:text-md sm:pl-16 md:pl-20 lg:text-lg';

  function nextSlide(event) {
    slideNo += 1;
  }

  function prevSlide(event) {
    slideNo -= 1;
  }
</script>

<div
  class="h-screen bg-red-800 transform absolute inset-0 w-screen about-detail
  text-gray-500 z-20"
>
  {#if slideNo === 0}
    <section in:fly="{flyIn}" out:fade="{fadeOut}" class="{sectionClass}">
      <div class="w-4/5 max-w-lg flex flex-col">
        <h2 class="sm:whitespace-pre-line">
          I'm a self-taught web developer lived in Indonesia. I started coding
          at age of 14 with BASIC in middle school, but I never learn it
          afterwards. I started fall in
          <span
            class="italic font-semibold text-xl rounded-lg"
            style="color:hotpink; box-shadow: 0 0 0 2px; padding: 0 10px;"
          >
            love
          </span>
          with code again when I'm forty years old, I know it seems a bit too
          late, but better late than never. Currently I'm looking for a remote
          job for a
          <span class="font-semibold" style="color: mediumspringgreen;">
            Frontend or Fullstack Engineer.
          </span>
        </h2>
        <ArrowRight on:click="{nextSlide}" className="{'w-10 h-10 self-end'}" />
      </div>
    </section>
  {:else if slideNo === 1}
    <section in:fly="{flyIn}" out:fade="{fadeOut}" class="{sectionClass}">
      <div class="w-4/5 max-w-lg flex flex-col">
        <h2 class="mb-2 font-bold">My web stacks:</h2>
        <ul class="mb-2 grid-container">
          {#each stacks as stack}
            <li>
              <div class="bg"></div>
              {stack}
            </li>
          {/each}
        </ul>
        <div class="flex justify-between w-full">
          <ArrowLeft
            on:click="{prevSlide}"
            className="{'w-10 h-10 self-start'}"
          />
          <ArrowRight
            on:click="{nextSlide}"
            className="{'w-10 h-10 self-end'}"
          />
        </div>
      </div>
    </section>
  {:else}
    <section in:fly="{flyIn}" out:fade="{fadeOut}" class="{sectionClass}">
      <div class="w-4/5 max-w-lg flex flex-col">
        <h2 class="mb-2 font-bold">
          <a
            class="cert-link"
            href="https://bit.ly/2Ls9nXC"
            target="_blank"
            rel="noopener noreferrer"
          >
            Certification:
          </a>
        </h2>
        <ul class="list-disc list-inside mb-2">
          {#each certs as cert}
            <li>
              {cert.course} by
              <span class="font-semibold text-gray-100">{cert.org}</span>
            </li>
          {/each}
        </ul>
        <ArrowLeft
          on:click="{prevSlide}"
          className="{'w-10 h-10 self-start'}"
        />
      </div>
    </section>
  {/if}
</div>