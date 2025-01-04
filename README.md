# How to Call API to Read

This document provides a step-by-step guide to read JSON files hosted on GitHub using both the **Raw URL** method and the **GitHub API**.

---

## **1. Using the Raw URL**
This is the simplest and most efficient way to fetch a JSON file.

### **Steps:**
1. Navigate to your JSON file on GitHub.
2. Click the **"Raw"** button to get the direct raw URL of the file.
3. Use this URL to fetch the JSON data.

### **Example:**

#### **Raw URL for Blum.json:**
```plaintext
https://raw.githubusercontent.com/TraiLuoi/DataGame/main/Blum.json
```

#### **Code Snippets:**

- **Using Axios (Node.js):**
```javascript
const axios = require('axios');

axios.get('https://raw.githubusercontent.com/TraiLuoi/DataGame/main/Blum.json')
  .then(response => {
    console.log(response.data); // JSON data
  })
  .catch(error => {
    console.error('Error fetching JSON:', error);
  });
```

- **Using Fetch (Browser):**
```javascript
fetch('https://raw.githubusercontent.com/TraiLuoi/DataGame/main/Blum.json')
  .then(response => response.json())
  .then(data => {
    console.log(data); // JSON data
  })
  .catch(error => {
    console.error('Error fetching JSON:', error);
  });
```

---

## **2. Using GitHub API**
This method fetches the file content through GitHub’s REST API. It is useful if you need additional metadata about the file or if the repository is private.

### **API Endpoint:**
```plaintext
https://api.github.com/repos/TraiLuoi/DataGame/contents/Blum.json
```

### **Steps:**
1. Send a GET request to the API endpoint.
2. Decode the `content` field from Base64 to retrieve the JSON data.

### **Code Snippets:**

- **Using Axios (Node.js):**
```javascript
const axios = require('axios');

axios.get('https://api.github.com/repos/TraiLuoi/DataGame/contents/Blum.json')
  .then(response => {
    const content = Buffer.from(response.data.content, 'base64').toString('utf-8');
    console.log(JSON.parse(content)); // JSON data
  })
  .catch(error => {
    console.error('Error fetching JSON from API:', error);
  });
```

- **Using Fetch (Browser):**
```javascript
fetch('https://api.github.com/repos/TraiLuoi/DataGame/contents/Blum.json')
  .then(response => response.json())
  .then(data => {
    const content = atob(data.content); // Decode Base64
    console.log(JSON.parse(content)); // JSON data
  })
  .catch(error => {
    console.error('Error fetching JSON from API:', error);
  });
```

---

## **When to Use Each Method**
| Method          | Use Case                                                                                     |
|-----------------|----------------------------------------------------------------------------------------------|
| **Raw URL**     | Simple and quick; suitable for public repositories where you just need the file content.     |
| **GitHub API**  | Useful for private repositories or when you need additional metadata about the file.         |

---

## **Notes:**
- For private repositories, include your GitHub Personal Access Token in the request header when using the API.
- Ensure that the file size does not exceed the GitHub API’s limit (1MB for file content).

---

Feel free to reach out if you encounter any issues or have questions about the setup!

