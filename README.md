<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Search Example</title>
  <style>
    /* Simple styling for the list and search input */
    #search-input {
      width: 200px;
      padding: 8px;
      margin-bottom: 20px;
    }
    #results {
      margin-top: 20px;
      list-style-type: none;
      padding: 0;
    }
    #results li {
      padding: 5px;
      border: 1px solid #ddd;
      margin-bottom: 5px;
    }
  </style>
</head>
<body>

  <h1>Search by Name or Email</h1>

  <input type="text" id="search-input" placeholder="Search by name or email..." />
  
  <ul id="results"></ul>

  <script>
    // Data to be validated and searched
    const data = [
      { name: 'John Doe', email: 'john@example.com' },
      { name: 'Jane Smith', email: 'jane@example.com' },
      { name: 'John Doe', email: 'john@example.com' }, // Duplicate
      { name: '', email: 'invalid@example.com' }, // Invalid name
      { name: 'Alice', email: 'bob@example.com' },
      { name: 'John Doe', email: 'unique@example.com' }
    ];

    // Step 1: Validate the data
    function validateData(arr) {
      const nameSet = new Set();
      const emailSet = new Set();
      const result = [];
      let invalidCount = 0;
      let duplicateCount = 0;

      arr.forEach((item) => {
        const { name, email } = item;

        if (!name || !email || typeof name !== 'string' || typeof email !== 'string') {
          invalidCount++;
        } else {
          if (nameSet.has(name) || emailSet.has(email)) {
            duplicateCount++;
          } else {
            nameSet.add(name);
            emailSet.add(email);
            result.push(item);
          }
        }
      });

      return { result, invalidCount, duplicateCount };
    }

    // Step 2: Search function
    function searchItems(validItems, searchTerm) {
      if (searchTerm.length < 2) {
        return validItems; // Return full list if search term is less than 2 characters
      }
      
      // Filter items based on name or email matching the search term
      return validItems.filter(item => 
        item.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
        item.email.toLowerCase().includes(searchTerm.toLowerCase())
      );
    }

    // Step 3: Handle input event
    const { result: validItems } = validateData(data); // Get validated items
    const searchInput = document.getElementById('search-input');
    const resultsContainer = document.getElementById('results');

    searchInput.addEventListener('input', (event) => {
      const searchTerm = event.target.value; // Get search term from input field
      const filteredResults = searchItems(validItems, searchTerm); // Filter based on search

      // Clear previous results
      resultsContainer.innerHTML = '';

      // Display filtered results
      filteredResults.forEach(item => {
        const listItem = document.createElement('li');
        listItem.textContent = `Name: ${item.name}, Email: ${item.email}`;
        resultsContainer.appendChild(listItem);
      });
    });
  </script>

</body>
</html>
