# Alpine.js for the newsroom

## Intro

During our innovation meeting, our development team explored the potential benefits of adopting Alpine.js for the newsroom. In this demo, you can read how and why it could potentially add value to our workflow.

### WHY
- Smaller codebase
- HTML in one place
- Faster to write and maintain

### Why not
- An extra external dependency

## Demo Alpine.js vs pure Javascript

### Mobile header

Pure Javascript
```
<nav>
  <button id="hamburger">Hamburger</button>
  <ul id="navlinks">
    <li>Link</li>
    <li>Link</li>
    <li>Link</li>
  </ul>
</nav>

<script>
  const hamburgerButton = document.querySelector('#hamburger')
  const navlinks = document.querySelector('#navlinks')

  hamburgerButton.addEventListener('click', () => {
    hamburgerButton.classList.toggle('is-hamburger')
    navlinks.classList.toggle('is-visible')
  })

  document.body.addEventListener('click', event => {
    if (!event.target.closest('#navlinks')) {
      navlinks.classList.add('hidden')
    }
  })
</script>

<style>
  .hidden {
    display: none;
  }
</style>
```

Alpine.js
```
<nav x-data="{ isOpen: false }">
  <button :class="isOpen ? 'close-icon' : 'haburger-icon'" @click="isOpen = !isOpen">Hamburger</button>
  <ul :class="isOpen ? '' : 'hidden'" @click.away="isOpen = false" x-show.transition="true">
    <li>Link</li>
    <li>Link</li>
    <li>Link</li>
  </ul>
</nav>
```

#### Noticable benefits

 - The Alpine.js header only has html files. That can be pretty handy when you want to create a new rebrand header, becausse you don't need to check if the old styles and javascript need to be removed.
 - The Pure Javascript file has more lines of code, even though the the Alpine.js file already includes a transition animation, while for the Javascript file more code needs to be added if you want to add that part too.
 - In Alpine.js, just by reading the html file it's clear which elements do something and which ones are not interactive.

 #### Working example

 Checkout [this codepen](https://codepen.io/norwindijkman/pen/poOvEKN) link or try this code for a working example:

 ```
 <!-- https://www.smashingmagazine.com/2020/03/introduction-alpinejs-javascript-framework/ -->
<!-- https://github.com/alpinejs/alpine -->

<script src="https://cdn.jsdelivr.net/gh/alpinejs/alpine@v2.x.x/dist/alpine.js" defer></script>


<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Alpine Toolbox - Example - Responsive Navbar</title>
    <link
      href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css"
      rel="stylesheet"
    />
    <script
      src="https://cdn.jsdelivr.net/gh/alpinejs/alpine@v2.3.5/dist/alpine.min.js"
      defer
    ></script>
  </head>

  <body class="bg-gray-300">
    <nav
      class="flex items-center justify-between flex-wrap p-6 fixed w-full z-10 top-0"
      x-data="{ isOpen: false }"
      @keydown.escape="isOpen = false"
      :class="{ 'shadow-lg bg-indigo-900' : isOpen , 'bg-gray-800' : !isOpen}"
    >
      <!--Logo etc-->
      <div class="flex items-center flex-shrink-0 text-white mr-6">
        <a
          class="text-white no-underline hover:text-white hover:no-underline"
          href="#"
        >
          <span class="text-2xl pl-2"
            ><i class="em em-grinning"></i> Brand McBrandface</span
          >
        </a>
      </div>

      <!--Toggle button (hidden on large screens)-->
      <button
        @click="isOpen = !isOpen"
        type="button"
        class="block lg:hidden px-2 text-gray-500 hover:text-white focus:outline-none focus:text-white"
        :class="{ 'transition transform-180': isOpen }"
      >
        <svg
          class="h-6 w-6 fill-current"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
        >
          <path
            x-show="isOpen"
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M18.278 16.864a1 1 0 0 1-1.414 1.414l-4.829-4.828-4.828 4.828a1 1 0 0 1-1.414-1.414l4.828-4.829-4.828-4.828a1 1 0 0 1 1.414-1.414l4.829 4.828 4.828-4.828a1 1 0 1 1 1.414 1.414l-4.828 4.829 4.828 4.828z"
          />
          <path
            x-show="!isOpen"
            fill-rule="evenodd"
            d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"
          />
        </svg>
      </button>

      <!--Menu-->
      <div
        class="w-full flex-grow lg:flex lg:items-center lg:w-auto"
        :class="{ 'block shadow-3xl': isOpen, 'hidden': !isOpen }"
        @click.away="isOpen = false"
        x-show.transition="true"
      >
        <ul
          class="pt-6 lg:pt-0 list-reset lg:flex justify-end flex-1 items-center"
        >
          <li class="mr-3">
            <a
              class="inline-block py-2 px-4 text-white no-underline"
              href="#"
              @click="isOpen = false"
              >Active
            </a>
          </li>
          <li class="mr-3">
            <a
              class="inline-block text-gray-600 no-underline hover:text-gray-200 hover:text-underline py-2 px-4"
              href="#"
              @click="isOpen = false"
              >link
            </a>
          </li>
          <li class="mr-3">
            <a
              class="inline-block text-gray-600 no-underline hover:text-gray-200 hover:text-underline py-2 px-4"
              href="#"
              @click="isOpen = false"
              >link
            </a>
          </li>
          <li class="mr-3">
            <a
              class="inline-block text-gray-600 no-underline hover:text-gray-200 hover:text-underline py-2 px-4"
              href="#"
              @click="isOpen = false"
              >link
            </a>
          </li>
        </ul>
      </div>
    </nav>

    <!--Container for content-->
    <div class="container shadow-lg mx-auto bg-white mt-24 md:mt-18"></div>
  </body>
</html>

 ```