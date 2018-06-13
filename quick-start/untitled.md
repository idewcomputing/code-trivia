# CSS

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
{% endcode-tabs-item %}
{% endcode-tabs %}

