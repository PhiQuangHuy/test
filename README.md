<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="list-container" style="height: 400px; overflow-y: auto;">
        <ul id="item-list">
        </ul>
      </div>
</body>
</html>

<script>
const data = Array.from({ length: 10000 }, (v, i) => ({
  id: i,
  name: `Item ${i + 1}`,
  checked: false
}));
console.log(data);


// This will store the IDs of checked items
const checkedItems = new Set();

// Virtual scrolling settings
const listContainer = document.getElementById('list-container');
const itemList = document.getElementById('item-list');
const itemHeight = 30; // Height of each item (in pixels)
const buffer = 5; // Number of items to buffer above and below the viewport

// To keep track of currently visible items
let visibleItems = [];

// Function to render visible items
function renderVisibleItems() {
  const containerHeight = listContainer.offsetHeight;
  const totalItems = data.length;
  const visibleCount = Math.ceil(containerHeight / itemHeight);
  const startIndex = Math.max(0, Math.floor(listContainer.scrollTop / itemHeight) - buffer);
  const endIndex = Math.min(totalItems, startIndex + visibleCount + buffer);

  visibleItems = data.slice(startIndex, endIndex);

  // Clear the current list
  itemList.innerHTML = '';

  // Render each visible item
  visibleItems.forEach(item => {
    const listItem = document.createElement('li');
    listItem.style.height = `${itemHeight}px`;
    listItem.innerHTML = `
      <input type="checkbox" data-id="${item.id}" ${checkedItems.has(item.id) ? 'checked' : ''} />
      ${item.name}
    `;
    itemList.appendChild(listItem);
  });
}

// Function to toggle checked state
function handleCheckboxChange(event) {
  const itemId = parseInt(event.target.getAttribute('data-id'), 10);

  if (event.target.checked) {
    checkedItems.add(itemId);
  } else {
    checkedItems.delete(itemId);
  }
}

// Attach event listener for scroll to implement virtual scrolling
listContainer.addEventListener('scroll', renderVisibleItems);

// Attach event listener for checkbox state change
itemList.addEventListener('change', handleCheckboxChange);

// Initial render
renderVisibleItems();

</script>
