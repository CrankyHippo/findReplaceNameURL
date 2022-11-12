# Find Name and Attach URL

This is a script I wrote to find and replace employee names and attach a URL using Google Apps Script.

```javascript

// List object with key pairs for name and assigned url
const list = [
  {
    name: "Bryan Burnett",
    url: "https://bryanburnett.com",
  },
];


function replaceTextWithUrl() {
  // Loop through list
  for (let i in list) {
    let searchText = list[i].name;
    let replaceText = list[i].name;
    let replaceUrl = list[i].url;
    
    // Get doc and body information
    const document = DocumentApp.getActiveDocument();
    const body = document.getBody();
    let search = null;
    
    // While search text matches name in list
    while ((search = body.findText(searchText, search))) {
      // Capture just name in the body
      const searchElement = search.getElement();
      const startIndex = search.getStartOffset();
      const endIndex = search.getEndOffsetInclusive();
      
      // Replace with matching text
      const textElement = searchElement.asText();
      textElement.deleteText(startIndex, endIndex);
      textElement.insertText(startIndex, replaceText);
      // Insert url with matched name
      textElement.setLinkUrl(
        startIndex,
        startIndex + replaceText.length - 1,
        replaceUrl
      );
    };
  };
};

```
