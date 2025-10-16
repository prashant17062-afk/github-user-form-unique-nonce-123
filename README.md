GitHub Account Creation Date Checker

## Summary
This project is a simple web application that allows users to fetch and display the account creation date of any public GitHub user. Built with Bootstrap for a clean and responsive user interface, the application uses the GitHub API to retrieve user data and presents the creation date in a standardized YYYY-MM-DD UTC format. It is designed to be a high-quality student submission, demonstrating fundamental web development concepts including API interaction, form handling, and date formatting.

## Setup
To run this application, you only need a modern web browser.
1.  **Save the file:** Save the provided `index.html` content into a file named `index.html` on your local machine.
2.  **Open in browser:** Open the `index.html` file using any web browser (e.g., Chrome, Firefox, Safari). You can simply double-click the file, or open your browser and navigate to `file:///path/to/your/index.html`.

No server-side setup or additional installations (like Node.js, npm, etc.) are required as it's a static HTML page with client-side JavaScript.

## Usage
1.  **Open the application:** Launch `index.html` in your web browser.
2.  **Enter a GitHub username:** In the input field labeled "e.g., torvalds", type the GitHub username of the account you wish to query.
3.  **Get Date:** Click the "Get Date" button.
4.  **View Result:** The account creation date will appear below the form in YYYY-MM-DD UTC format.
5.  **Error Handling:** If the username is not found, or there's an issue with the GitHub API (e.g., rate limiting), an appropriate error message will be displayed.

### Optional Token Usage
The application can optionally use a GitHub Personal Access Token (PAT) for API requests. While the public account creation date typically doesn't require authentication, providing a token can help bypass GitHub API rate limits for unauthenticated requests.

To use a token, append `?token=YOUR_GITHUB_TOKEN` to the URL in your browser's address bar. Replace `YOUR_GITHUB_TOKEN` with your actual PAT. For example:
`file:///path/to/your/index.html?token=ghp_YOURTOKENHERE`
(Note: For security, it's generally not recommended to expose tokens directly in URLs, but this demonstrates the capability as requested.)

## Main Code Logic
The core functionality resides in the `<script>` block within `index.html`:

1.  **DOM Content Loaded:** The JavaScript execution is deferred until the entire HTML document is loaded, ensuring all elements are available.
2.  **Form Submission Handling:** An event listener is attached to the form (`id="github-user-unique-nonce-123"`) for the `submit` event. It prevents the default form submission (which would refresh the page).
3.  **Username Input:** The value from the input field (`id="github-username-input"`) is captured as the GitHub username.
4.  **Optional Token Check:** The code parses the browser's URL query parameters (`window.location.search`) to check for a `token` parameter. If found, this token is included in the `Authorization` header of the fetch request as `token YOUR_GITHUB_TOKEN`.
5.  **GitHub API Request:**
    *   The `fetchGitHubCreationDate` asynchronous function constructs the GitHub API endpoint URL: `https://api.github.com/users/USERNAME`.
    *   It performs a `fetch` request to this URL, optionally including the `Authorization` header if a token was provided.
    *   It handles various HTTP response statuses:
        *   `404 Not Found`: Indicates the username does not exist.
        *   `403 Forbidden` (especially with `X-RateLimit-Remaining: 0` header): Indicates API rate limit exhaustion.
        *   Other non-OK responses trigger a generic error.
    *   If the response is successful, the JSON data is parsed.
6.  **Date Extraction and Formatting:**
    *   The `created_at` field from the API response (e.g., "2008-01-14T04:33:35Z") is used to create a `Date` object.
    *   The `toISOString().split('T')[0]` method is used to format this date into the required `YYYY-MM-DD` string, ensuring it is in UTC.
7.  **Display Result:** The formatted date is then displayed in the `p` element with `id="github-created-at"`. Error messages are displayed in the `div` with `id="form-feedback"`.

## License
This project is open-source and available under the MIT License. You are free to use, modify, and distribute the code for personal or commercial purposes, provided the original copyright and license notice are included.

## Contact
For any questions, feedback, or suggestions, please feel free to reach out.
Developer: Expert AI Web Developer
Email: ai.developer@example.com (Placeholder)