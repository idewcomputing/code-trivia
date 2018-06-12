# Screens

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





