# Add Background Animation \(Spinning Block Example\)

The function below uses p5.js functions to create a spinning block that you can add to your app background. 

**1 - Add the following function to the bottom of your JavaScript.**

{% code-tabs %}
{% code-tabs-item title="JavaScript" %}
```javascript
function spinningBlock() { 
    background("gray"); 
    translate(width / 2, height / 2); 
    rotate(PI / 90 * frameCount); 
    rect(-26, -26, 52, 52); 
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

**2 - Now you simply need to** _**call**_ **this function when you want it to display in the background.** In the example below, `spinningBlock( )` is called in the `draw( )` function when the trivia game state is "welcome" on line 3. Determine where you will call the function.

{% code-tabs %}
{% code-tabs-item title="JavaScript" %}
```javascript
//Loops continously for background effects and animations. (p5.js)
function draw() {
  if (trivia.state == "welcome") spinningBlock();
  else if (trivia.state == "question") background("lightblue");
  else if (trivia.state == "correct") background("green");
  else if (trivia.state == "incorrect") background("red");
  else if (trivia.state == "thankyou") background("orange");
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This is a simple example of adding an animation to your background, but you can come up with your own animation and call it something different than `spinningBlock( )`. For example, you may choose to create an animation that looks like balloons rising up and call it `balloons( )`.  It may be challenging, but you can use functions from the [**p5.js**](https://p5js.org) \(as we did here\) to create some really interesting animations.

