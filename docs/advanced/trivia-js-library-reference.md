# Trivia JS Library Reference

{% hint style="info" %}
The information on this page is in development and is provided for advanced use of the library.
{% endhint %}

## Trivia Methods

### trivia.loadGoogleSheet\(link\)

Used to load a question bank from a Google Sheet.

### trivia.getCategories\(\)

Returns all category names in an array.

### trivia.getUnfinishedCategories\(\)

Returns category names of the categories having unanswered questions. Returns as an array.

### trivia.gotoNextQuestion\(\)

Advances the trivia game to the next question.

### trivia.insertCategoryInfo\(\)

This function places a button for each category into the HTML.

### trivia.insertQuestionInfo\(\)

This function puts the current question and answers taken from your database into the HTML to be displayed.

### trivia.shuffleAnswers\(\)

This function shuffles the multiple choice answers so that the correct answer does not always show at the top.

### trivia.startClickListeners\(\)

This function simply starts the event listeners for different types of player clicks.

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

This provides the current question's index in the questions array.

### trivia.totalQuestions

The provides the total questions in the game.

### trivia.totalCorrect

This provides how many correct answers the player has at the moment.

### trivia.totalAnswered

This provides how many questions have been answered by the player at that moment.

### trivia.state

This provides the state of the game. Possible states -- 'welcome', 'question', 'correct', 'incorrect', and 'thankyou'.

## Raw Library JavaScript

```javascript
var trivia = {
  questions: [],
  currentCategory: null,
  categoriesEnabled: false,
  currentQuestion: {},
  questionIndex: 0,
  totalQuestions: 0,
  totalCorrect: 0,
  totalAnswered: 0,
  state: "welcome",
  loadGoogleSheet: function (link) {
    return new Promise((resolve, reject) => {
      var self=this;
      Papa.parse(link, {
        download: true,
        header: true,
        complete: function (results) {
          self.questions = results.data;
          console.log("Questions loaded: ",self.questions);
          self.questions = shuffle(self.questions);
          if (self.questions.length) self.currentQuestion = self.questions[0];
          self.questionIndex = 0;
          self.totalQuestions = self.questions.length;
          self.totalCorrect = 0;
          self.totalAnswered = 0;
          self.state = "welcome";
          self.startClickListeners();
          resolve("success");
        }
      })
    });
  },
  getCategories: function () {
    var cats = [];
    this.questions.filter((q) => {
      if (!cats.includes(q.category)) cats.push(q.category);
    });
    return cats;
  },
  getUnfinishedCategories: function () {
    var cats = [];
    this.questions.filter((q) => {
      if (!cats.includes(q.category) && !q.response) cats.push(q.category);
    });
    return cats;
  },
  gotoNextQuestion: function () { //this just forwards a "deprecated function"
    displayQuestion();
  },
  insertCategoriesInfo: function () {
    var cats = this.getCategories();
    var unfcats = this.getUnfinishedCategories();
    $('#category-set').html('');
    cats.forEach((c) => {
      var $catbtn = $(`<button class="category-btn">${c}</button>`);
      if (unfcats.includes(c)) {
        $catbtn.on('click', function (e) {
          trivia.currentCategory = c;
          onClickedCategory();
        });
      }
      else $catbtn.attr("disabled", true);
      $('#category-set').append($catbtn);
    })
  },
  insertQuestionInfo: function () {
    trivia.state = "question";
    $(".answer-btn").attr("disabled", null);
    trivia.questionIndex = trivia.questions.findIndex((q) => {
      if (!this.categoriesEnabled) return !q.response;
      else return !q.response && q.category == this.currentCategory;
    });
    if (trivia.questions[trivia.questionIndex]) {
      trivia.currentQuestion = trivia.questions[trivia.questionIndex];
      for (var prop in trivia.currentQuestion) {
        $("#" + prop).html(trivia.currentQuestion[prop]);
      }
    }
    else {
      if (this.totalAnswered == this.totalQuestions) {
        trivia.state = "thankyou";
        displayThankyou(); //game over
      }
      else if (this.categoriesEnabled) {
        trivia.state = "categories";
        displayCategories();
      }
      else alert('Yikes');
    }
  },
  shuffleAnswers: function () {
    $("#answer-set").html(shuffle($("#answer-set").children())); //shuffle answers
  },
  startClickListeners: function () {
    //listen for answer button clicks
    $(".screen").on("click", ".answer-btn", ev => {
      $(".answer-btn").attr("disabled", "disabled"); //turn off buttons to prohibit cheating :)
      trivia.triggerAnswer($(ev.target).is("#correctAnswer"));
    });

    //listen for restart button click
    $(".screen").on("click", ".start-btn", ev => {
      this.questions.forEach(function (q) { delete q.response });
      trivia.questionIndex = 0;
      if (!this.categoriesEnabled) trivia.state = "question";
      else trivia.state = "categories";
      trivia.currentQuestion = trivia.questions[0]; //reset to the first question
      onClickedStart();
    });
  },
  triggerAnswer: function (correct) {
    $(".answer-btn").attr("disabled", "disabled");
    if (correct) {
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
  }
};

```

## Quick Start for Code Template

Copy the HTML/CSS/JavaScript below to get started immediately. 

{% tabs %}
{% tab title="index.html" %}
```markup
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>repl.it</title>
    <link href="style.css" rel="stylesheet" type="text/css" />
  </head>
  <body>
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
    <script src="https://cdn.jsdelivr.net/gh/idewcomputing/code-trivia/src/trivia.js"></script> <!-- iDEW trivia -->

    <script src="code.js"></script>
  </body>
</html>
```
{% endtab %}

{% tab title="style.css" %}
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
{% endtab %}

{% tab title="code.js" %}
```javascript
//Runs once at the beginning
function setup() {
  var googleSheetLink = "https://docs.google.com/spreadsheets/d/e/2PACX-1vRYCi4KENeZMlf9JbV8BhVrdOHse2250INSiRo7gEYWUYp3V0jiWFKWcnm1jzx5q1BMsmd9fOopk2Z_/pub?output=csv";
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
{% endtab %}
{% endtabs %}

