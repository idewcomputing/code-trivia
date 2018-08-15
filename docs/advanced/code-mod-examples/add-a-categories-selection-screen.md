# Add a Categories Selection Screen

Let's add a screen for the player to choose a question category after they click start.

**1 - Add the following HTML in your** _**index.html**_ **file just after your** _**welcome screen**_**.** This provides a place for the iDEW trivia library to place buttons for your categories.

```markup
<!-------------- CATEGORY SCREEN --------------->
	<div class='screen' id='category-screen'>
		<h1>Choose a category.</h1>
    	<div id="category-set">
    	</div>
	</div>
```

**2 - Enable trivia categories in your** _**code.js**_ **file by placing the following Javascript line inside your `setup( )` function.** This simply tells the iDEW trivia library that you would like to process your category screen.

```javascript
trivia.categoriesEnabled = true;
```

**3 - Add the following Javascript function in your** _**code.js**_ **file after \(not inside\) your `displayWelcome( )` function.** 

```javascript
function displayCategories() {
  $(".screen").hide();
  $("#category-screen").show();
  trivia.insertCategoriesInfo();
}
```

4 - **Modify your current `onClickedStart( )` function to include `displayCategories()`, shown on line 2 below.** You should remove `displayQuestion()`line inside your onClickedStart\(\).  You simply want the player to see your categories screen after clicking start, instead of going straight to the question screen.

```javascript
function onClickedStart() {
  displayCategories();
}
```

**5 - Lastly, add a new Javascript function to handle what to do when a category is selected.** In this case you will just move the player on to the question screen. The iDEW trivia library is keeping track of what category was selected. To keep things tidy, place this new function just before \(but not inside\) your `onClickedStart( )` function.

```javascript
function onClickedCategory() {
  displayQuestion();
}
```

That's it. Try it out.

