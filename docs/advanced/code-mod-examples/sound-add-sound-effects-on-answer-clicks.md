# Add Sound Effects on Answer Clicks

Let's add some simple sound effects to your trivia game when a player answers a question. 

**1 - Find sound effects you would like to use or make your own.** Files of type _.mp3_ are a good choice for web apps. You can download the two sounds below as a starting point. 

{% file src="../../.gitbook/assets/sound\_correct.mp3" caption="sound\_correct.mp3" %}

{% file src="../../.gitbook/assets/sound\_incorrect.mp3" caption="sound\_incorrect.mp3" %}

**2 - Create a folder named `sounds` and place your sound files in it.** Pay close attention to your files and folder structure for you app. Below is an example of what yours should look like.

* index.html
* style.css
* code.js
* **sounds**
  * sound\_correct.mp3
  * sound\_incorrect.mp3

**3 - Declare variables for your sounds at the very top of your** _**code.js**_ **file.** They should be above the `setup()` function. These lines create variables that will _represent_ your sound files so that you can play them at a later point in your code. Also, since we are placing them at the top of your code and not inside any function, they are called _global variables_. This means we can access these variables inside any other function, which we will do next.

```javascript
var soundCorrect = new Audio("sounds/sound_correct.mp3");
var soundIncorrect = new Audio("sounds/sound_incorrect.mp3");
```

**4 - Place the code shown below inside your `onClickedAnswer( )` function to play the sounds at the appropriate time.** Notice how we are combining the text and sound feedback in our _if/else_ statements inside the code brackets `{ }`. Your text feedback will likely be different. So adjust as needed. 

```javascript
  if (isCorrect) {
    $("#feedback").html(`Way to go!`).show();
    soundCorrect.play();
  }
  else {
    $("#feedback").html(`Better luck next time.`).show();
    soundIncorrect.play();
  }
```

That's it. Your game should now play your sound effects when a player answers a question.

{% hint style="info" %}
If you are using a longer sound file, like a song, you will want to know about the following two features.

**pause\( \)** - This method will pause your sound. For example, `soundCorrect.pause( );`

**currentTime** - This property can be used to reset the sound to the beginning. For example, `soundCorrect.currentTime = 0;`
{% endhint %}

\`\`

