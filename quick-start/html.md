# HTML

{% code-tabs %}
{% code-tabs-item title="HTML" %}
```markup
<!-------------- WELCOME SCREEN --------------->
<div class='screen' id='welcome-screen'>
    <h1>Welcome to our example game!</h1>
    <h4>You have questions waiting for you.</h4>
    <button class="start-btn">Start</button>
</div>

<!-------------- QUESTION SCREEN --------------->
<div class='screen' id='question-screen'>
  <h4 id="category">Category Name</h4>
  <h1 id="question">Question goes here?</h1>
  <div class="answer-set">
    <button class="answer-btn" id="correctAnswer">Correct Answer</button>
    <button class="answer-btn" id="incorrectAnswer1">Wrong Answer</button>
    <button class="answer-btn" id="incorrectAnswer2">Wrong Answer</button>
    <button class="answer-btn" id="incorrectAnswer3">Wrong Answer</button>
  </div>
  <h1 id="feedback">Feedback will go here.</h1>
</div>

<!-------------- THANK YOU SCREEN --------------->
<div class='screen' id='thankyou-screen'>
  <h1>Thanks for playing our game!</h1>
  <h4 id='game-results'>Looks like you did pretty well.</h4>
  <button class="start-btn">Restart</button>
</div>

<!-- JS Libraries -->
<script src='https://cdnjs.cloudflare.com/ajax/libs/tabletop.js/1.5.1/tabletop.min.js'></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js'></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.6.1/p5.min.js'></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.6.1/addons/p5.dom.min.js'>
</script>
<script src='https://codepen.io/jlyst/pen/mKmKoP.js'></script>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

