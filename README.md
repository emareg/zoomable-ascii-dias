# Zoomable ASCII Diagrams
ASCII diagrams are great. They can be easily copied and displayed in all environments that support monofont text. However, larger diagrams can easily overflow the width of the text area which results in broken diagrams when text wraping is enabled.

As a remedy, we use the following JS snippet to adjust the font size, such that the diagram always fits the screen width. If you click on it, you get the full size.


```js
const baseFontSize = 12

function getContentWidth (element) {
    var styles = getComputedStyle(element)

    return element.clientWidth
        - parseFloat(styles.paddingLeft)
        - parseFloat(styles.paddingRight)
}
function getTextWidth(el) {    
    // text = document.getElementById("test"); 
    text = document.createElement("pre"); 
    document.body.appendChild(text); 

    text.style.font = "var(--font-c)"; 
    text.style.fontSize = baseFontSize; 
    text.style.height = 'auto'; 
    text.style.width = 'auto'; 
    text.style.position = 'absolute'; 
    text.style.whiteSpace = 'no-wrap'; 
    text.innerHTML = el.innerHTML; 

    width = Math.ceil(text.scrollWidth); 
    document.body.removeChild(text); 
    return width
} 
function updateDiaWidth (diagram) {
    const diaTextWidth = getTextWidth(diagram) + 1;
    const diaElementWidth = getContentWidth(diagram) - 1;
    if (diaElementWidth < diaTextWidth){
        let fontSize = (diaElementWidth / diaTextWidth) * baseFontSize;
        diagram.style.fontSize = `${fontSize}px`;
    }
}
```

