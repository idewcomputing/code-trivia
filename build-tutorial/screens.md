# 1. Screens as Containers

### HTML for the Screen Containers

Below you see the HTML for the three screen "containers". We will add more detail to each screen later. Notice that each screen has `class='screen'` . This will allow us to easily change the style \(CSS\) of all three screens later in the same way. Also, notice that each screen has a unique `id` that will allow us to target each screen in a particular way later. You will notice that the page preview is not too exciting, but should contain text from all three screens.

**Copy the HTML code and paste it into a new** [**CodePen's HTML**](https://codepen.io/pen/) **\(or another code editor inside the `<body>`\).**

{% code-tabs %}
{% code-tabs-item title="HTML" %}
```markup
<!-------------- WELCOME SCREEN --------------->
<div class='screen' id='welcome-screen'>
  <h1>Welcome screen.</h1>
</div>

<!-------------- QUESTION SCREEN --------------->
<div class='screen' id='question-screen'>
  <h1>Question screen.</h1>
</div>

<!-------------- THANK YOU SCREEN --------------->
<div class='screen' id='thankyou-screen'>
  <h1>Thank you screen.</h1>
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### CSS for the Body and Screens

Let's add a little style to our screens next. Notice how the `body` , which contains all contents of the page, is given a background color of "gray" and a margin of "0". This gives us a nice edge-to-edge background for placing our screen content. 

Next you will see several styles being applied to screens, since `.screen` affects all elements with that class. Notice how `background-color` uses `rgba( )` so that we can "see through" the screen a bit to the background. You will want this feature later. The rest of the styling has to do with sizing the screens and content in a way that fits nicely on any device, and you will probably want to leave these elements alone.

Copy the CSS code into your CodePen's CSS and notice the change. You will need to scroll the preview down to see all the screens now.

{% code-tabs %}
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
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Make Modifications and Save

1. Add at least two more styles to the `.screen` selector. Below are some useful CSS styles to try.
   * [border](https://www.w3schools.com/cssref/pr_border.asp)
   * [border-radius](https://www.w3schools.com/cssref/css3_pr_border-radius.asp)
   * [box-shadow](https://www.w3schools.com/cssref/css3_pr_box-shadow.asp)
   * [color](https://www.w3schools.com/cssref/pr_text_color.asp) - for text color
   * [font-family](https://www.w3schools.com/CSSref/css_websafe_fonts.asp)
   * [background-color with rgba\( \)](https://www.w3schools.com/cssref/func_rgba.asp) - if you want to modify the current color.
2. **Save your Code for the next step!**



