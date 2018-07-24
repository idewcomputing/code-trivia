# Animation: Spinning Block

The function below uses p5.js functions to create a spinning block that you can add to your app background. **Add the following function to the bottom of your JavaScript.**

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

Now you simply need to _call_ this function when you want it to display in the background. **In the example below, spinningBlock\(\) is called in the `draw()` function when trivia game state is "welcome" on line 3.**

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

