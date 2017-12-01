## Website Performance Optimization portfolio project

We have a task to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques we have came across in the [Critical Rendering Path course](https://www.udacity.com/course/ud884) and performance-related issues so that it achieves a target PageSpeed score of 90 and runs at 60 frames per second.

### Result
[page speed score](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fpratiksharagit.github.io%2Fweb-performance%2F&tab=desktop)


### Getting started

Some useful tips to help you get started:

1. Check out the repository
2. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

3. Open a browser and visit localhost:8080
4. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

5. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)


### CRITICAL RENDERING PATH

#### Part 1: Optimize PageSpeed Insights score 

To view the portfolio website download all the files and open index.html in your browser.

1. Made the Google Analytics script at the bottom of the body so it doesn't block rendering.
2.Replaced the non-critical Javascript such as Google Font CSS file request to JS script at the bottom of the body, so downloading the fonts won't block rendering.
3. Made the CSS inline in order to not block the page rendering.


#### Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher.

#### Optimizing the Scrolling

I made the following changes in order to optimize the scrolling:

1. The updatePositions function had calculations within a loop that were redundant and could be moved outside of the loop. This prevents the browser from having to render the page every time the loop iterates.
2. The updatePositions function used the CSS left property to move the pizzas. By changing this to the CSS transform property, it no longer triggered layout or paint in the timeline.
3. Modified the code to calculate the number of pizzas needed to fill the webpage based on browser inner dimensions.
4. Cached the needed DOM elements so that the brower isn't querying the DOM every time the for loops are iterated in the updatePositions function


#### Optimizing the Pizza Resizing

I made the following changes to optimize the pizza resizing:

1. The changePizzaSlices function was using an inefficient selector to get all of the pizza elements. I changed it to select by element type and saved the elements in an array.
2. The changePizzaSlices had a very inefficient for loop. I moved some calculations out of the for loop.
3.Cached the needed DOM elements so that the brower isn't querying the DOM every time the for loops are iterated in the changePizzaSizes function.

These changes resulted in the resizing going from ~200 ms to < 7 ms.


