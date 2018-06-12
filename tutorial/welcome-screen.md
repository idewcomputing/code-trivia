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



```text
body {
  margin: 0;
}

h1, h4 {
  text-align: center;
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

button:empty {
   display: none;
}

.highlight {
  background-color: green;
  color: white;
}

.answer-set {
  background-color: rgba(0,0,0,.05);
  border-radius: 19px;
  padding: 5%;
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

```text
<!-------------- WELCOME SCREEN --------------->
<div class='screen' id='welcome-screen'>
  <h1>Welcome to our example game!</h1>
  <h4>You have
    <span id='totalQuestions'>-</span> questions waiting for you.</h4>
  <button class="start-btn">Start</button>
</div>


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

<!-------------- THANK YOU SCREEN --------------->
<div class='screen' id='thankyou-screen'>
  <h1>Thanks for playing our game!</h1>
  <h4>You got <span id="totalCorrect">-</span> of <span id="totalAnswered">-</span> questions correct.</h4>
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

```text
//Runs once at the beginning
function setup() {
  var googleSheetLink = "1B3RFU17Y3gE7hcsarU81TM7FPudDTmt0OJz2vws4uw4";
  trivia.loadGoogleSheet(googleSheetLink).then(displayWelcome); 
}

//Loops continously for background effects and animations. (p5.js)
function draw() {
  if (trivia.state == "welcome") background("yellow");
  else if (trivia.state == "question") background("lightblue");
  else if (trivia.state == "correct") background("green");
  else if (trivia.state == "incorrect") background("red");
  else if (trivia.state == "thankyou") background("orange");
}

function displayWelcome() {
  $(".screen").hide();
  $("#welcome-screen").show();
  $("#totalQuestions").html(trivia.totalQuestions);
}

function displayQuestion() {
  $(".screen").hide();
  $("#question-screen").show();
  $("#correctAnswer").removeClass("highlight");
  $("#feedback").hide();
  trivia.insertQuestionInfo();
  trivia.shuffleAnswers();
}

function displayThankyou() {
  $(".screen").hide();
  $("#thankyou-screen").show();
  $("#totalCorrect").html(trivia.totalCorrect);
  $("#totalAnswered").html(trivia.totalAnswered);
}

function onClickedAnswer(isCorrect) {
  if (isCorrect) $("#feedback").html(`Way to go!`).show();
  else $("#feedback").html(`Better luck next time.`).show();
  $("#correctAnswer").addClass("highlight"); //highlight right answer
  setTimeout(trivia.gotoNextQuestion, 3000); //wait 3 secs...next question
}

function onClickedStart() {
  displayQuestion();
}
```

