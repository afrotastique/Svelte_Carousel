<script lang="ts">
import EmblaCarousel, { type EmblaOptionsType } from 'embla-carousel'
import { addPrevNextBtnsClickHandlers } from '../components/EmblaCarouselArrowButtons'
import { addDotBtnsAndClickHandlers } from '../components/EmblaCarouselDotButton'
import '../styles/base.css'
import '../styles/sandbox.scss'
import '../styles/embla.scss'
import { onMount } from 'svelte';

const OPTIONS: EmblaOptionsType = { slidesToScroll: 'auto' }

  let emblaNode;
  let viewportNode;
  let prevBtnNode;
  let nextBtnNode;
  let dotsNode;

  onMount(() => {
    emblaNode = document.querySelector('.embla');
    viewportNode = emblaNode.querySelector('.embla__viewport');
    prevBtnNode = emblaNode.querySelector('.embla__button--prev');
    nextBtnNode = emblaNode.querySelector('.embla__button--next');
    dotsNode = emblaNode.querySelector('.embla__dots');
    
    const emblaApi = EmblaCarousel(viewportNode, OPTIONS)

const removePrevNextBtnsClickHandlers = addPrevNextBtnsClickHandlers(
  emblaApi,
  prevBtnNode,
  nextBtnNode
)
const removeDotBtnsAndClickHandlers = addDotBtnsAndClickHandlers(
  emblaApi,
  dotsNode
)

emblaApi.on('destroy', removePrevNextBtnsClickHandlers)
emblaApi.on('destroy', removeDotBtnsAndClickHandlers)
  });    
</script>

  <html lang="en" class="theme-dark">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>Embla Carousel Slides To Scroll Vanilla</title>
  </head>

  <body>
    <header>
      <h1 class="header">Embla Carousel Slides To Scroll Vanilla</h1>
    </header>

    <section class="embla">
      <div class="embla__viewport">
        <div class="embla__container">
          <div class="embla__slide">
            <div class="embla__slide__number">1</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">2</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">3</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">4</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">5</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">6</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">7</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">8</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">9</div>
          </div>
          <div class="embla__slide">
            <div class="embla__slide__number">10</div>
          </div>
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

        <div class="embla__dots"></div>
      </div>
    </section>

    <footer class="footer">
    
    </footer>

    <noscript> You need to enable JavaScript to run this app. </noscript>
  </body>
</html>
  
