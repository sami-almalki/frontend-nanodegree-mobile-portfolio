## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository and inspect the code.

### Getting started

#### Part 1: Optimize PageSpeed Insights score for index.html

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

#### Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher. You will find instructive comments in main.js.

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>

### Optimizations made to the project
In order to achieve an acceptable `PageSpeed` score for Mobile and Desktop, I've done the following steps:
1. Minified and compressed large assets.
2. Optimized the `Critical Rendering Path` and eliminated `Render-Blocking` JavaScript and CSS:
  * Inlined `Above-The-Fold` style to avoid render-blocking for CSS.
  * Used `async` to avoid parser-blocking for JavaScript.

In addition, I've made optimizations to `views/js/main.js` to avoid causing `Forced Synchronous Layout` in `changePizzaSizes()` function:
1. Removed the `determineDx()` function as it is not efficient.
2. Added the slider value calculator in `changePizzaSizes()` instead of `determineDx()`.
3. Removed the layout calls by using `%` instead of fixed `px`.
4. Eliminated the need to recalculate style after layout call over and over.
5. Moved the redundant DOM selector out of the loop and assigned it to a variable.
6. Used the faster `getElementsByClassName()` instead of `querySelectorAll()`.

Moreover, to render the Pizzeria website with a consistent frame-rate at `60fps` when scrolling, I've made the following modifications to `views/js/main.js`:
1. Moved the `scrollTop` layout call out of the loop to avoid `Forced Synchronous Layout`.
2. Used the faster `translateX()` instead of changing the `left` property.
3. Used a function `scrollIt()` and a global variable `isScrolling` to fire the animation.
4. Used `requestAnimationFrame()` to animate properly.
5. Used the faster `getElementsByClassName()` instead of `querySelectorAll()`.
6. Used the faster `getElementById()` instead of `querySelector()`.
7. Used `window.onscroll` instead of `addEventListener()`.
8. Splitted the loop into 2 loops, one for calculating `phases`, the other for positioning.
9. Minimized the number of sliding pizzas depending on height using `window.innerHeight`.

[Wanna test the code? Click here!](https://sami-almalki.github.io/frontend-nanodegree-mobile-portfolio/)
