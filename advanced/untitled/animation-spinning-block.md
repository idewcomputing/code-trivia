# Animation: Spinning Block

The function below uses p5.js functions to create a spinning block that you can add to your app background. **Add the following function to the bottom of your JavaScript.**

```javascript
function spinningBlock() { 
    background("gray"); 
    translate(width / 2, height / 2); 
    rotate(PI / 90 * frameCount); 
    rect(-26, -26, 52, 52); 
}
```

Now you simply need to call this function when you want it to display in the background. **In the example below, spinningBlock\(\) is called in the `draw()` function during the welcome screen on line 3.**

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

