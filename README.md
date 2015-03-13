## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).


####Part 1: Optimize PageSpeed Insights score for index.html

Production version of the website can be accessed at the following link:
http://drewman7.github.io/frontend-nanodegree-mobile-portfolio/

Source code can be accessed at the following (via github):
https://github.com/drewman7/frontend-nanodegree-mobile-portfolio

Based on PageSpeed, index.html was optimized to 93/100 for Mobile and 94/100 for Desktop.  To accomplish this, the following changes were made:

-- External javascript files files were set to load asynchronous so they did not block rendering
-- Critical css in style.css was brought inline to minimize redering blocking which was everything
-- Removed external load of font and placed it in as inline css
-- Set the print.css to a media type of print, so it isn't loaded until necessary 



####Part 2: Optimize Frames per Second in pizza.html

Production version of the website can be accessed at the following link:
http://drewman7.github.io/frontend-nanodegree-mobile-portfolio/views/pizza.html

Source code can be accessed at the following (via github):
https://github.com/drewman7/frontend-nanodegree-mobile-portfolio/views

Based on Google developer tools, pizza.html was optimized paint at under 60 FPS per second on average.  

Also, each frame takes approximately 0.04 to 0.08 ms to generate.

To accomplish this, the following changes were made to main.js:

Global Variables
-- Global variables were setup to hold the pizza element information so it wouldn't have to be determined each update

addEventListner Function
-- Number of floating pizzas were reduced from 200 to 50 since 200 are not needed.  Well under 50 are visiable at a given time
-- Staic element attributes were added for the i % 5 calculation

updatePostions Function
-- Math.sin calculation was broken up.  The 'i % 5' calcuation was moved to the inital element setup so it is calculated only once when the element is initially created
-- The Math.sin calculation based on scoll location was moved outside of the for loop so it is only calculated once when updatePositions is called
-- To accomplish the above, sin(x + y) was replaced with sin(x)*cos(y) + sin(y)*cos(x) based on the mathmatical properies of sin(x+y).  This math function ends up taking place over 3 functions
-- The 'for' loop was moved to a separate function so it could be called by the requestAnimationFrame
-- requestAnimationFrame calls moveThePizzas function thus allowing for the elements to be updated before repainting

moveThePizzas Function
-- This function contains the 'for' loop that runs through each element of the global variable to update the position
-- The original Math.sin function is completed by adding the scroll based piece of the calculation to the individual element pieces (var phase = phaseSin * items[i].cos + phaseCos * items[i].sin)
-- Each element is moved based on the phase calculation above
-- Since this function was called by the requestAnimationFrame, the position updates are not painted to the screen until this function is complete