# Display: Custom Feedback Text

If you want to provide special feedback for each trivia question after the answer to provide more information for the player on that question topic, there are two steps.

**Add a "feedback" column to your question spreadsheet \(our database\) like shown below, and add the custom feedback text for each question.**

![](../../.gitbook/assets/screen-shot-2018-06-19-at-11.02.39-am.png)

Next, you want to use the trivia property  `trivia.currentQuestion.feedback` . to place the text in the HTML element with the _id_="feedback". Notice how that is done in lines 2 and 4 below. **Make the same changes within your `onClickedAnswer` function in your JavaScript.**

```javascript
function onClickedAnswer(isCorrect) {
  if (isCorrect) $("#feedback").html(trivia.currentQuestion.feedback).show();
  // else $("#feedback").html(`Better luck next time.`).show();
  else $("#feedback").html(trivia.currentQuestion.feedback).show();
  $("#correctAnswer").addClass("highlight"); //highlight right answer
  setTimeout(trivia.gotoNextQuestion, 3000); //wait 3 secs...next question
}
```

