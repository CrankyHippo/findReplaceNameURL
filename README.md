# Find Name and Attach URL

This is a script I wrote to find and replace employee names and attach a URL using Google Apps Script.

```javascript

const list = [
  {
    name: "Bryan Burnett",
    url: "https://bryanburnett.com",
  },
];


function replaceTextWithUrl() {
  for (let i in list) {
    let searchText = list[i].name;
    let replaceText = list[i].name;
    let replaceUrl = list[i].url;

    const document = DocumentApp.getActiveDocument();
    const body = document.getBody();
    let search = null;

    while ((search = body.findText(searchText, search))) {
      const searchElement = search.getElement();
      const startIndex = search.getStartOffset();
      const endIndex = search.getEndOffsetInclusive();

      const textElement = searchElement.asText();
      textElement.deleteText(startIndex, endIndex);
      textElement.insertText(startIndex, replaceText);
      textElement.setLinkUrl(
        startIndex,
        startIndex + replaceText.length - 1,
        replaceUrl
      );
    };
  };
};

```
