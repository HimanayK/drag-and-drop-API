# drag-and-drop-API


# **HTML Drag and Drop API (Step by Step in Simple Words)**  

The **Drag and Drop API** lets you grab an item with your mouse and move it somewhere else on the page.  

#### Summary
1. Make an item draggable using ``` draggable="true"```.
2. Detect when dragging starts using ``` dragstart ```.
3. Allow dropping using ``` dragover ```.
4. Move the item to the new place using ``` drop ```.

---

## **Step 1: Make an Item Draggable**  
First, you need an element that can be dragged. You do this by adding the `draggable="true"` attribute.  

#### ✅ Example:  
```html
<p id="dragItem" draggable="true">Drag me!</p>
```
> Now, this paragraph can be dragged.
---

## **Step 2: Detect When Dragging Starts**  
You need to tell the browser what happens when you start dragging the item. This is done using the dragstart event in JavaScript.

#### ✅ Example:
```js
document.getElementById("dragItem").addEventListener("dragstart", function(event) {
    event.dataTransfer.setData("text", event.target.id); // Store the ID of the dragged item
});
```
> **What this does:**
>>When the dragging starts, we save the ID of the dragged item so we can use it later.

---

## **Step 3: Allow Dropping**
By default, items cannot be dropped into other elements. You need to allow dropping by using the dragover event.

#### ✅ Example:
```js
document.getElementById("dropArea").addEventListener("dragover", function(event) {
    event.preventDefault(); // This allows dropping
});
```
> **What this does:**
>> Without event.preventDefault(), the item cannot be dropped.

---
**
## **Step 4: Handle the Drop**
Now, when the item is dropped, we need to tell the browser what to do.

#### ✅ Example:
 ```js
document.getElementById("dropArea").addEventListener("drop", function(event) {
    event.preventDefault();
    let draggedItem = event.dataTransfer.getData("text"); // Get the ID of dragged item
    event.target.appendChild(document.getElementById(draggedItem)); // Move it to new place
});
```

> **What this does:**
>>It gets the ID of the dragged item.
It moves the item inside the drop area.

---

## **Step 5: Create a Drop Area**
You need a place to drop the item, like a div.

#### ✅ Example:
```html
<div id="dropArea" style="width: 200px; height: 200px; border: 2px dashed black;">
    Drop Here
</div>
```
---
---

## Full Working Example ⬇️
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Drag and Drop Example</title>
</head>
<body>

    <p id="dragItem" draggable="true">Drag me!</p>

    <div id="dropArea" style="width: 200px; height: 200px; border: 2px dashed black;">
        Drop Here
    </div>

    <script>
        // Step 2: Dragging starts
        document.getElementById("dragItem").addEventListener("dragstart", function(event) {
            event.dataTransfer.setData("text", event.target.id);
        });

        // Step 3: Allow dropping
        document.getElementById("dropArea").addEventListener("dragover", function(event) {
            event.preventDefault();
        });

        // Step 4: Handle the drop
        document.getElementById("dropArea").addEventListener("drop", function(event) {
            event.preventDefault();
            let draggedItem = event.dataTransfer.getData("text");
            event.target.appendChild(document.getElementById(draggedItem));
        });
    </script>

</body>
</html>
```

---
---

## Understanding dataTransfer.setData
The dataTransfer.setData(format, data) method is used to store data when dragging an item.

#### ✅ Example:
```js
event.dataTransfer.setData("text", event.target.id);
```
> - "text" → This is the format (can be "text/plain", "text/html", or "application/json").
> - event.target.id → Saves the ID of the dragged element so we can use it later when dropping.

---

## Role of preventDefault()
By default, the browser does not allow dropping into another element.
We use event.preventDefault(); to enable dropping.

#### ✅ Example:
```js
document.getElementById("dropArea").addEventListener("dragover", function(event) {
    event.preventDefault(); // Allows dropping
});
```

> **Why do we need it?**
>> - Inside the dragover event → It enables dropping.
>> - Inside the drop event → It prevents unwanted browser actions (like opening a file).
>>> 📝 Without ***preventDefault()***, the item won't be droppable.

---
## ✅ Full Flow
- When you start dragging → setData saves the ID.
- When you drop → getData retrieves that ID.
- appendChild moves the dragged element to the drop area.

---
---

# For my understanding only ---------

## Which Event is Considered in This Line?
```js
let draggedItem = event.dataTransfer.getData("text");
```
> - This line is inside the drop event listener.
> - It retrieves the data (ID of dragged item) stored earlier using setData.
> - This means it gets the ID of the dragged element when you drop it.
