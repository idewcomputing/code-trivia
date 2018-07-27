# Trivia JS Library Reference

{% hint style="info" %}
The information on this page is in development and is provided for advanced use of the library.
{% endhint %}

## Trivia Methods

### trivia.loadGoogleSheet\(link\)

### trivia.gotoNextQuestion\(\)

### trivia.insertQuestionInfo\(\)

### trivia.shuffleAnswers\(\)

### trivia.startClickListeners\(\)

## Trivia Objects and Attributes

### trivia.questions

This is an array of the trivia question objects.

### trivia.currentQuestion

This is the current trivia question object which contains key/value  pairs defined by the question database. For example, `trivia.currentQuestion.category` will contain the category label for the current question if it is available. The standard question object keys are below, but can be extended as needed. 

* category
* question
* correctAnswer
* incorrectAnswer1
* incorrectAnswer2
* incorrectAnswer3

### trivia.questionIndex

### trivia.totalQuestions

### trivia.totalCorrect

### trivia.totalAnswered

### trivia.state



## Raw Library JavaScript

```javascript
var trivia = {
  questions: [],
  currentQuestion: {},
  questionIndex: 0,
  totalQuestions: 0,
  totalCorrect: 0,
  totalAnswered: 0,
  state: "welcome",
  loadGoogleSheet: function(link) {
    return new Promise((resolve, reject) => {
      Tabletop.init({
        key: link,
        callback: data => {
          this.questions = data.Sheet1.elements;
          this.questions = shuffle(this.questions);
          if (this.questions.length) this.currentQuestion = this.questions[0];
          this.questionIndex = 0;
          this.totalQuestions = this.questions.length;
          this.totalCorrect = 0;
          this.totalAnswered = 0;
          this.state = "welcome";
          this.startClickListeners();
          resolve("success");
        }
      });
    });
  },
  advanceQuestion: function() {
    trivia.questionIndex++;
    trivia.state = "question";
    if (trivia.questions[trivia.questionIndex])
      trivia.currentQuestion = trivia.questions[trivia.questionIndex];
  },
  gotoNextQuestion: function() {
    trivia.advanceQuestion(); //advance counter to the next question
    $("button").attr("disabled", null);
    if (trivia.totalQuestions > trivia.questionIndex) displayQuestion();
    else {
      displayThankyou(); //game over
      trivia.state = "thankyou";
    }
  },
  insertQuestionInfo: function() {
    for (var prop in trivia.currentQuestion) {
      $("#" + prop).html(trivia.currentQuestion[prop]);
    }
  },
  shuffleAnswers: function() {
    $("#answer-set").html(shuffle($("#answer-set").children())); //shuffle answers
  },
  startClickListeners: function() {
    //listen for answer button clicks
    $(".screen").on("click", ".answer-btn", ev => {
      $("button").attr("disabled", "disabled"); //turn off buttons to prohibit cheating :)
      if ($(ev.target).is("#correctAnswer")) {
        trivia.currentQuestion.response = "correct";
        trivia.state = "correct";
      } else {
        trivia.currentQuestion.response = "incorrect";
        trivia.state = "incorrect";
      }
      trivia.totalCorrect = trivia.questions.filter(item => {
        return item.response == "correct";
      }).length;
      trivia.totalAnswered = trivia.questions.filter(item => {
        return item.response;
      }).length;
      onClickedAnswer(trivia.currentQuestion.response == "correct");
    });

    //listen for restart button click
    $(".screen").on("click", ".start-btn", ev => {
      trivia.questionIndex = 0;
      trivia.state = "question";
      trivia.currentQuestion = trivia.questions[0]; //reset to the first question
      onClickedStart();
    });
  }
};
```

## Quick Start for Code Template

Copy the HTML/CSS/JavaScript below to get started immediately. 

{% hint style="warning" %}
**CodePen Ready Code**

The HTML is ready for CodePen, but if you are using another code editor, it will need to be placed within the &lt;body&gt; of a standard HTML page that properly loads the CSS and JS files.
{% endhint %}

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
  <div id="answer-set">
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
<script src='https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.6.1/addons/p5.dom.min.js'></script>
<script src='https://codepen.io/jlyst/pen/mKmKoP.js'></script>
```
{% endcode-tabs-item %}

{% code-tabs-item title="CSS" %}
```css
body {
  margin: 0;
  background-color: gray;
}

.screen {
  background-color: rgba(255,255,255,.5);
  box-sizing: border-box;
  margin: 15px auto;
  padding: 15px;
  max-width: 700px;
  width: calc(100vw - 30px);
  height: calc(100vh - 30px);
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

.highlight {
  background-color: green;
  color: white;
}

canvas {
  min-width: 100vw;
  min-height: 100vh; 
  position: absolute;
  top: 0;
  z-index: -1;
}
```
{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}
```javascript
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
  $("#game-results").html(`You got ${trivia.totalCorrect} of ${trivia.totalAnswered} correct.`);
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
{% endcode-tabs-item %}
{% endcode-tabs %}

