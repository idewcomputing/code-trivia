# Support True/False Questions

### CSS

In order to display basic True/False questions, simply add the following CSS to your stylesheet. `:empty` identifies answer buttons that have no content and hides the element using `display: none` 

```css
.answer-btn:empty {
   display: none;
} 
```

### Google Sheet Table of Questions

In your Google sheet table simply put the correct answer \(whether "True" or "False"\) in the correct answer column and the incorrect \(whether "False" or "True"\) in the first incorrect column. Leave the remaining two answers blank. 

Likewise, you could have questions that offer only 3 multiple choice answers.

