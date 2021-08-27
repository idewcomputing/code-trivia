# Managing the Question DB

{% embed url="https://www.loom.com/share/585749188d1d4799891d55c5718df244" %}

## Using Google Sheet as Database \(Recommended\)

1. Login to Google Drive.
2. Go to [this spreadsheet](https://docs.google.com/spreadsheets/d/1r58warugRYIwFIAkH2rk4h7OboZnDe1l5C23EXn4nY0/edit?usp=sharing).
3. Create your own copy of the spreadsheet by selecting `File > Make a copy...`.
4. Now publish your copy of the spreadsheet by selecting `File > Publish to the web...` and click the `Publish` button.
5. Once your spreadsheet is published, click the _**share**_ button \(upper right-hand side\) of the spreadsheet page and copy the shareable link. \(Make sure your link is set to _**Anyone with the link can view**_.\)
6. Find the setup\(\) function in your JavaScript file, like the example below, and replace your link as the `googleSheetLink`. Actually, you only need the long key in your link, but the full URL should work as well.
7. Now you can edit your Google Sheet and your question database will automatically be updated in your trivia app.

```javascript
//Runs once at the beginning
function setup() {
  var googleSheetLink = "1B3RFU17Y3gE7hcsarU81TM7FPudDTmt0OJz2vws4uw4";
  trivia.loadGoogleSheet(googleSheetLink).then(displayWelcome); 
}
```

