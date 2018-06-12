# Welcome Screen

{% code-tabs %}
{% code-tabs-item title="HTML" %}
```markup
<!-- WELCOME SCREEN -->
<div class='screen' id='welcome-screen'>
  <h1>Welcome to our example trivia game!</h1>
  <h4>Twenty great questions await you.</h4>

  <button class="start-btn">Start</button>
</div>

<!-- JS Libraries -->
<script src='https://codepen.io/jlyst/pen/mKmKoP.js'></script> //the trivia library
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="CSS" %}
```css
body {

  margin: 0;
}

button {
  background-color: rgba(255,255,255,.7);
  border: none;
  outline: none;
  border-radius: 19px;
  box-shadow: 3px 3px 7px black;
  font-size: 24px;
  display: block;
  margin: 10px auto;
  min-height: 70px;
  width: 100%;
}

.screen {
  box-sizing: border-box;
  box-shadow: 3px 3px 7px black;
  margin: 15px auto;
  padding: 15px;
  background-color: rgba(255,255,255,.5);
  border-radius: 15px;
  max-width: 700px;
  width: calc(100vw - 30px);
  height: calc(100vh - 30px);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```markup
<!-------------- QUESTION SCREEN --------------->
<div class='screen' id='question-screen'>
  <h4 id="category"></h4>
  <h1 id="question"></h1>
  <div class="answer-set">
    <button class="answer-btn" id="correctAnswer"></button>
    <button class="answer-btn" id="incorrectAnswer1"></button>
    <button class="answer-btn" id="incorrectAnswer2"></button>
    <button class="answer-btn" id="incorrectAnswer3"></button>
  </div>
  <h1 id="feedback"></h1>
</div>
```



