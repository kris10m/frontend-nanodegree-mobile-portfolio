## Website Performance Optimization portfolio project

I accepted Udacity's challege to optimize Cameron's online portfolio for speed!

### Getting started

####Part 1: Optimize PageSpeed Insights score for index.html

Instead of using ngrok, I opted to use GitHub pages to host and test the site.  

After checking out the repository, creating the gh-pages version, and inspecting the site in Chrome Canary (web and mobile versions), I began the iterative process of profiling, optimizing, and measuring index.html.  Details are below.

The steps I followed to optimize index.html are as follows:
1: Ran baseline of initial page speed at https://developers.google.com/speed/pagespeed/insights.  Result was 28/100
2: Compressed and reduced size of the pizzeria.jpg (2315KB) and profilepic.jpg (15KB) files
  a) using http://www.jpegmini.com/ ... producing 2 new files pizzeria_mini.jpg (769KB) and profilepic_mini.jpg (12KB)
  b) I then resized pizzeria_mini.jpg in MSPaint to 25% of the original size... pizzeria_miniV2.jpg (130KB), and again to V2 by 50%... resulting in pizzeria_miniV3.jpg (54KB)
3: Updated index.html and views/pizza.html to use the compressed/resized version of pizzeria_miniV3.jpb
4: Updated index.html to use the compressed/resized version of profilepic_mini.jpg
5: Prevented JS rendor blocking by adding async to goolge analytics api
6: Inlined css/style.css and moved google api and css/print.css to end to improve performance in index.html
7: Reran the page speed at https://developers.google.com/speed/pagespeed/insights.  Result was 93/100!!!

The optimized version of index.html is here: http://kris10m.github.io/frontend-nanodegree-mobile-portfolio/


####Part 2: Optimize Frames per Second in pizza.html

After inspecting views/pizza.html and views/js/main.js, I began the iterative process of profiling, optimizing, and measuring views/pizza.html.  Details are below.

The steps I followed to optimize views/pizza.html and views/js/main.js are as follows:
1: Ran baseline of initial page speed at https://developers.google.com/speed/pagespeed/insights.  Result was 77/100
2: Inlined views\css\style.css in pizza.html
3: Prevented JS rendor blocking by adding async at the end of the main.js reference in pizza.html
4: Reran the page speed at https://developers.google.com/speed/pagespeed/insights.  Result was 87/100!
5: Inspected timeline using Chrome DevTools.  Results showed determineDx, changePizzaSizes, and resizePizza functions in main.js had the heaviest stack > 400ms each.
6: Inspected console using Chrome DevTools. Time to resize pizzas resulted in > 145ms.  Average time to generate last 10 frames ranged between .09ms and .16ms.
7: Streamlined the changePizzaSizes sub-function of the main resizePizza function, consistent with the syntax used in the other sub-functions and removed the dx variable which was useless before.
8: Re-inspected timeline of pizza.html using Chrome DevTools.  Results showed a more optimal scripting and improvements in the resizePizza and changePizzaSizes functions in main.js. The heaviest stack < 3ms each.
9: Re-inspected console of pizza.html using Chrome DevTools. Time to resize pizzas resulted in ~1ms.  Average time to generate last 10 frames ranged between .10ms and .44ms.

The optimized version of pizza.html is here: http://kris10m.github.io/frontend-nanodegree-mobile-portfolio/views/pizza.html


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
* <a href="https://developers.google.com/speed/webp/docs/compression">***NEW: Tips on compressing images</a>
* <a href="https://developers.google.com/speed/docs/insights/BlockingJS">***NEW: Tips on preventing JS render blocking</a>
* <a href="https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery">***NEW: Tips on optimizating CSS</a>

### Other useful sites I found Googling :-)
* <a href="http://www.imageoptimizer.net/Pages/Home.asp">Easy to use image compression tool, though it did not reduce the size of my images</a>
* <a href="http://www.jpegmini.com/ ">Better image compressor... This one worked!</a>
* <a href="http://lea.verou.me/2011/10/easily-keep-gh-pages-in-sync-with-master/">Quick tip on syncing your GitHub master branch with gh-pages</a>

