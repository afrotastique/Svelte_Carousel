<script lang="ts">
import EmblaCarousel, {type EmblaOptionsType, type EmblaCarouselType} from 'embla-carousel'
import { addPrevNextBtnsClickHandlers } from '../components/EmblaCarouselArrowButtons'
import { addDotBtnsAndClickHandlers } from '../components/EmblaCarouselDotButton'
import Autoplay from 'embla-carousel-autoplay'
import '../styles/main.scss'
import '../styles/carousel.scss'
import { onMount } from 'svelte';

const OPTIONS: EmblaOptionsType = { loop: true }


  let emblaNode;
  let viewportNode;
  let prevBtnNode;
  let nextBtnNode;
  let dotsNode;

  // slide content
  let slides = [
    { imageUrl: '/empireState.jpg', altText: 'Empire State Building', 
    overlayText: 'Empire State',
    videoUrl: './newYork.mp4'  },
    { imageUrl: '/Paris.jpg', altText: 'Eiffel Tower', overlayText: 'Eiffel Tower',
      videoUrl: './Paris.mp4'
     },
    { imageUrl: '/aquarium.jpg', altText: 'Aquarium', overlayText: 'Aquarium',
      videoUrl: './aquarium.mp4'
     },
    { imageUrl: '/ripley.jpg', altText: "Ripleys's", overlayText: "Ripley's",
      videoUrl: './ripley.mp4'
     },
    { imageUrl: '/mountain.jpg', altText: 'Mountain', overlayText: 'Mountain',
      videoUrl: './mountain.mp4'
     },
    { imageUrl: '/cafe.jpg', altText: 'Cafe', overlayText: 'Cafe',
      videoUrl: './cafe.mp4'
     },
     { imageUrl: '/plane.jpg', altText: 'Plane', overlayText: 'Plane',
      videoUrl: './plane.mp4'
     },
  ];

// playVideo and pauseVideo
const playVideo = (event) => {
    event.target.play();
  };

  const pauseVideo = (event) => {
    event.target.pause();
  };

  onMount(() => {
    emblaNode = document.querySelector('.embla');
    viewportNode = emblaNode.querySelector('.embla__viewport');
    prevBtnNode = emblaNode.querySelector('.embla__button--prev');
    nextBtnNode = emblaNode.querySelector('.embla__button--next');
    
    // autoplay stop on hover needs work
    const emblaApi = EmblaCarousel(viewportNode, OPTIONS, [Autoplay({stopOnMouseEnter: true, stopOnInteraction: false})])

    const onNavButtonClick = (emblaApi: EmblaCarouselType): void => {
      const autoplay = emblaApi?.plugins()?.autoplay;
      if (!autoplay) return;

      const resetOrStop =
        autoplay.options.stopOnInteraction === false
        ? autoplay.reset
        : autoplay.stop;

      resetOrStop();
    };   


    const removePrevNextBtnsClickHandlers = addPrevNextBtnsClickHandlers(
      emblaApi,
      prevBtnNode,
      nextBtnNode
    );

    emblaApi.on('destroy', removePrevNextBtnsClickHandlers);
    emblaApi.on('destroy', removeDotBtnsAndClickHandlers);
  });

</script>

  <html lang="en" class="theme-dark">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>Svelte Carousel</title>
  </head>

  <body>
    <header>
      <h1 class="header">EYDS SvelteKit Exercise</h1>
    </header>

    <section class="embla">
        <div class="embla__viewport">
          <div class="embla__container">
            {#each slides as slide}
              <div class="embla__slide">
                <img class="card_image" src={slide.imageUrl} alt={slide.altText} />
                {#if slide.overlayText}
                  <div class="overlay-text">
                    <h3>{slide.overlayText}</h3>
                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quos molestiae at illum.</p> 
                    <button class="button" on:click="{() => window.location.href = 'https://example.com'}">
                      Learn More</button> 
                  </div>
                  <div class="video_card">
                    <video class="video" src={slide.videoUrl} on:mouseenter={playVideo} on:mouseleave={pauseVideo}  muted loop></video>
                  </div>
                {/if}
              </div>
            {/each}
          </div>
        </div>

      <div class="embla__controls">
        <div class="embla__buttons">
          <button class="embla__button embla__button--prev" type="button">
            <svg class="embla__button__svg" viewBox="0 0 532 532">
              <path
                fill="currentColor"
                d="M355.66 11.354c13.793-13.805 36.208-13.805 50.001 0 13.785 13.804 13.785 36.238 0 50.034L201.22 266l204.442 204.61c13.785 13.805 13.785 36.239 0 50.044-13.793 13.796-36.208 13.796-50.002 0a5994246.277 5994246.277 0 0 0-229.332-229.454 35.065 35.065 0 0 1-10.326-25.126c0-9.2 3.393-18.26 10.326-25.2C172.192 194.973 332.731 34.31 355.66 11.354Z"
              ></path>
            </svg>
          </button>

          <button class="embla__button embla__button--next" type="button">
            <svg class="embla__button__svg" viewBox="0 0 532 532">
              <path
                fill="currentColor"
                d="M176.34 520.646c-13.793 13.805-36.208 13.805-50.001 0-13.785-13.804-13.785-36.238 0-50.034L330.78 266 126.34 61.391c-13.785-13.805-13.785-36.239 0-50.044 13.793-13.796 36.208-13.796 50.002 0 22.928 22.947 206.395 206.507 229.332 229.454a35.065 35.065 0 0 1 10.326 25.126c0 9.2-3.393 18.26-10.326 25.2-45.865 45.901-206.404 206.564-229.332 229.52Z"
              ></path>
            </svg>
          </button>
        </div>

      </div>
    </section>

    <footer class="footer">
    
    </footer>

    <noscript> You need to enable JavaScript to run this app. </noscript>
  </body>
</html>
  
