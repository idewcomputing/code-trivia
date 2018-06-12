# Welcome Screen

{% code-tabs %}
{% code-tabs-item title="HTML" %}
```markup
<!-------------- WELCOME SCREEN --------------->
<div class='screen' id='welcome-screen'>
  <h1>Welcome to our example game!</h1>
  <h4>You have 20 questions waiting for you.</h4>
  <button class="start-btn">Start</button>
</div>
```
{% endcode-tabs-item %}

{% code-tabs-item title="CSS" %}
```css
body {
  margin: 0;
}

button {
  outline: none;
  font-size: 24px;
  display: block;
  margin: 10px auto;
  min-height: 70px;
  width: 100%;
}

.screen {
  box-sizing: border-box;
  margin: 15px auto;
  padding: 15px;
  background-color: rgba(255,255,255,.5);
  max-width: 700px;
  width: calc(100vw - 30px);
  height: calc(100vh - 30px);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

