# Trivia Library Reference

## Trivia Methods

### trivia.loadGoogleSheet\(\)

### trivia.advanceQuestion\(\)

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

