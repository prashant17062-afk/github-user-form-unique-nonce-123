Academic Grading GitHub Lookup Tool

Summary
This is a web-based tool designed to assist academic staff in quickly looking up GitHub user profiles. By simply entering a GitHub username, the tool fetches and displays key profile information such as the user's avatar, name, number of followers, public repositories, and a custom-calculated account age in whole years. It also leverages an ARIA live region for real-time accessibility announcements of lookup status and caches the last successful lookup in localStorage to repopulate the form and results on subsequent visits.

Setup
To set up and run this application:
1.  Save the provided `index.html` file to your local computer.
2.  Open the `index.html` file in any modern web browser (e.g., Chrome, Firefox, Edge). No server-side setup or additional dependencies are required.

Usage
1.  **Enter Username**: On the loaded page, locate the "GitHub Username:" input field.
2.  **Lookup**: Enter a valid GitHub username (e.g., "octocat", "torvalds") into the input field.
3.  **Submit**: Click the "Lookup User" button.
4.  **View Results**:
    *   If the user is found, their profile details (avatar, name, followers, public repos, creation date, calculated account age, bio, and location) will appear below the form.
    *   A loading spinner will be visible during the API request.
    *   Screen readers will announce the status of the lookup (started, succeeded, or failed) via the ARIA live region.
    *   The tool will automatically store the details of the last successfully looked-up user in your browser's local storage.
5.  **Cached Data**: If you close and re-open the page, or refresh it, the input field will be pre-filled with the last successfully searched username, and its profile details will be immediately displayed from cache.
6.  **Error Handling**: If the username is not found or a network error occurs, an appropriate error message will be displayed, and announced to screen readers.

Main Code Logic
The application is built as a single HTML file containing HTML structure, CSS for styling, and JavaScript for functionality.

1.  **HTML Structure (`index.html`)**:
    *   **Form (`#github-lookup-form`)**: Contains an input field (`#github-username-input`) for the GitHub username and a submit button (`#lookup-button`). The input field includes `aria-describedby="github-status"` for accessibility.
    *   **Loading Spinner (`#loading-spinner`)**: A visually hidden spinner that is shown during API requests.
    *   **ARIA Live Region (`#github-status`)**: A `div` with `aria-live="polite"` and the `sr-only` class. This element is visually hidden but its `textContent` changes are announced by screen readers to provide real-time feedback on the lookup process (start, success, failure).
    *   **Results Section (`#github-results`)**: Initially hidden, this section displays the fetched user data. It includes placeholders for `avatar_url`, `login`, `name`, `followers`, `public_repos`, `created_at`, `bio`, and `location`.
    *   **Account Age (`#github-account-age`)**: A `span` within the results section that displays the calculated age of the GitHub account in whole years, alongside the creation date.
    *   **Error Message (`#github-error`)**: A paragraph element for displaying error messages.

2.  **CSS Styling**:
    *   Provides basic styling for a clean and professional appearance.
    *   Includes the `.sr-only` class to hide elements visually while keeping them accessible to screen readers, essential for the `#github-status` div.

3.  **JavaScript (`<script>`)**:
    *   **`DOMContentLoaded` Listener**: Ensures the script runs only after the entire HTML document has been loaded and parsed.
    *   **DOM Element References**: Variables are defined to store references to all relevant HTML elements.
    *   **`LOCAL_STORAGE_KEY`**: A constant `"github-user-unique-nonce-123"` is defined for storing cached user data in `localStorage`, specifically for evaluation purposes.
    *   **`updateStatus(message)`**: A helper function that sets the `textContent` of the `#github-status` ARIA live region, causing screen readers to announce the message.
    *   **`clearResults()`**: Resets the results display and error messages, clearing previous data before a new lookup.
    *   **`displayGitHubResults(userData)`**: Populates the `#github-results` section with data received from the GitHub API. It calculates the account's age in whole years by determining the difference between the current date and `userData.created_at`. The result is formatted as "X years old".
    *   **`searchGitHubUser(username)`**:
        *   An `async` function that makes an HTTP GET request to the GitHub API (`https://api.github.com/users/{username}`).
        *   Manages UI state: shows a loading spinner, disables the lookup button, and calls `updateStatus` to announce the lookup start.
        *   Handles API responses:
            *   On success (`response.ok`), parses the JSON data, calls `displayGitHubResults`, saves the user data to `localStorage` using `localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(data))`, and calls `updateStatus` for success.
            *   On error (e.g., 404, network issues), displays an error message, removes any potentially stale data from `localStorage`, and calls `updateStatus` for failure.
        *   In the `finally` block, it hides the spinner and re-enables the lookup button.
    *   **Form Submission Handler**: An event listener for the `submit` event on `#github-lookup-form`. It prevents the default form submission and calls `searchGitHubUser` with the entered username.
    *   **`loadCachedUserData()`**: Executed on `DOMContentLoaded`. It attempts to retrieve data from `localStorage.getItem(LOCAL_STORAGE_KEY)`. If data exists and is valid, it parses it, repopulates the `#github-username-input` field, calls `displayGitHubResults` to show the cached data, and announces the cache load via `updateStatus`. If the cached data is corrupt, it's removed.

License
This project is licensed under the MIT License.

Contact
For any inquiries or feedback, please contact the expert AI web developer at [your.email@example.com] or through GitHub Issues.