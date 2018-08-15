# Custom Feedback Text for Individual Questions

This is an example of how you can provide special feedback for each trivia question after the player answers. For example, you may want to provide more information on that question's topic whether they answered correctly or not.

**1 - Add a "feedback" column to your question spreadsheet \(our database\) like shown below, and add custom feedback text for each question.**

![](../../.gitbook/assets/screen-shot-2018-06-19-at-11.02.39-am.png)

 

**2 - Next, you want to use the trivia property  `trivia.currentQuestion.feedback` to place the text in the HTML element having** _**id**_**="feedback".** Notice how that is done in lines 2 and 3 below. Make the same changes within your `onClickedAnswer` function in your JavaScript.

{% code-tabs %}
{% code-tabs-item title="JavaScript" %}
```javascript
function onClickedAnswer(isCorrect) {
  if (isCorrect) $("#feedback").html(trivia.currentQuestion.feedback).show();
  else $("#feedback").html(trivia.currentQuestion.feedback).show();
  $("#correctAnswer").addClass("highlight"); //highlight right answer
  setTimeout(trivia.gotoNextQuestion, 3000); //wait 3 secs...next question
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

That's it. Try it out.

