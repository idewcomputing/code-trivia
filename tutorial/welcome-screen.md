# Welcome Screen

``` html
<!-- WELCOME SCREEN -->
<div class='screen' id='welcome-screen'>
  <h1>Welcome to our example trivia game!</h1>
  <h4>Twenty great questions await you.</h4>
  <button class="start-btn">Start</button>
</div>
```

``` css
body {
  margin: 0;
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

.screen {
  box-sizing: border-box;
  box-shadow: 3px 3px 7px black;
  margin: 15px auto;
  padding: 15px;
  background-color: rgba(255,255,255,.5);
  border-radius: 15px;
  max-width: 700px;
  width: calc(100vw - 30px);
  height: calc(100vh - 30px);
}
```

``` html
<!-- JS Libraries -->
<script src='https://codepen.io/jlyst/pen/mKmKoP.js'></script> //the trivia library
```
