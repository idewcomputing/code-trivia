# Display the Total Question Count at Welcome

In this simple mod we will let the player know at the welcome screen how many questions are in the database using the `trivia.totalQuestions` value that automatically counts the questions for us. 

**1 - Modify your** _**welcome screen**_ **HTML like on line 4 below, where the `id="question-count"` was added.**

{% code title="HTML" %}
```markup
<!-------------- WELCOME SCREEN --------------->
<div class='screen' id='welcome-screen'>
    <h1>Welcome to our example game!</h1>
    <h4 id="question-count">You have questions waiting for you.</h4>
    <button class="start-btn">Start</button>
</div>
```
{% endcode %}

Now we will insert the `trivia.totalQuestions` value into a sentence to be placed in the element with `id="question-count"`. 

**2- Add the code on line 4 below to the end of your `displayWelcome()` function in your JavaScript.**

{% code title="JavaScript" %}
```javascript
function displayWelcome() {
  $(".screen").hide();
  $("#welcome-screen").show();
  $("#question-count").html(`You have ${trivia.totalQuestions} questions waiting for you.`);
}
```
{% endcode %}

That's it. Try it out.

