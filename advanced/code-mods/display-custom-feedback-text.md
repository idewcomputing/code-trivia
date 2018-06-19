# Display: Custom Feedback Text

If you want to provide special feedback for each trivia question after the answer to provide more information for the player on that quetsion topic, there are two steps.

![](../../.gitbook/assets/screen-shot-2018-06-19-at-11.02.39-am.png)

```js
function onClickedAnswer(isCorrect) {
  if (isCorrect) $("#feedback").html(trivia.currentQuestion.feedback).show();
  // else $("#feedback").html(`Better luck next time.`).show();
  else $("#feedback").html(trivia.currentQuestion.feedback).show();
  $("#correctAnswer").addClass("highlight"); //highlight right answer
  setTimeout(trivia.gotoNextQuestion, 3000); //wait 3 secs...next question
}
```


