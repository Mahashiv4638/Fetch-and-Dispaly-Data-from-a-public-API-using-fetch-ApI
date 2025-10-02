# Fetch-and-Dispaly-Data-from-a-public-API-using-fetch-ApI
use Javascripty fetch API to get data from a public API and display it.
HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fetch User Data</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <h1>User Profiles 👤</h1>
    <div id="user-container">
        <p>Loading user data...</p>
    </div>

    <script src="script.js"></script>
</body>
</html>
## 2. CSS File (styles.css)
This file adds some styling to make the displayed data look clean and organized. We'll create a card-based layout for each user using a CSS grid.

CSS

body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    background-color: #f0f2f5;
    color: #333;
    padding: 20px;
    margin: 0;
}

h1 {
    text-align: center;
    color: #1c1e21;
    margin-bottom: 30px;
}

#user-container {
    display: grid;
    /* Create responsive columns that are at least 300px wide */
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
    max-width: 1200px;
    margin: 0 auto;
}

.user-card {
    background-color: #ffffff;
    border: 1px solid #dddfe2;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease-in-out;
}

.user-card:hover {
    transform: translateY(-5px);
}

.user-card h2 {
    margin-top: 0;
    color: #0056b3;
    font-size: 1.25em;
}

.user-card p {
    margin: 8px 0;
    font-size: 0.95em;
    color: #4b4f56;
}

.user-card a {
    color: #007bff;
    text-decoration: none;
}

.user-card a:hover {
    text-decoration: underline;
}
## 3. JavaScript File (script.js)
This is the core of the task. The script uses the fetch() function to send a GET request to the API. It then processes the JSON response and dynamically creates HTML elements to display the information for each user.

JavaScript

// Wait for the HTML document to be fully loaded before running the script
document.addEventListener('DOMContentLoaded', () => {

    const userContainer = document.getElementById('user-container');
    const apiUrl = 'https://jsonplaceholder.typicode.com/users';

    // Use the Fetch API to get data from the URL
    fetch(apiUrl)
        .then(response => {
            // Check if the request was successful (status code 200-299)
            if (!response.ok) {
                throw new Error(`HTTP error! Status: ${response.status}`);
            }
            // Parse the response body as JSON
            return response.json();
        })
        .then(users => {
            // Clear the initial "Loading..." message
            userContainer.innerHTML = '';

            // Loop through each user in the received data array
            users.forEach(user => {
                // Create a div element for the user card
                const userCard = document.createElement('div');
                userCard.className = 'user-card';

                // Populate the card with user information using template literals
                userCard.innerHTML = `
                    <h2>${user.name} (@${user.username})</h2>
                    <p><strong>Email:</strong> <a href="mailto:${user.email}">${user.email}</a></p>
                    <p><strong>Phone:</strong> ${user.phone}</p>
                    <p><strong>Website:</strong> <a href="http://${user.website}" target="_blank">${user.website}</a></p>
                    <p><strong>Company:</strong> ${user.company.name}</p>
                `;

                // Append the newly created user card to the container
                userContainer.appendChild(userCard);
            });
        })
        .catch(error => {
            // Handle any errors that occurred during the fetch operation
            console.error('Error fetching data:', error);
            userContainer.innerHTML = '<p>Sorry, we could not load the user data. Please try again later.</p>';
        });
});
