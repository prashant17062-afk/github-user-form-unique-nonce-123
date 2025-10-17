# GitHub Account Creation Date Finder

This project is a simple web application designed to fetch and display the account creation date of any public GitHub user. It's implemented as a single static HTML page, utilizing Bootstrap for a clean user interface and plain JavaScript to interact with the GitHub REST API.

## Features

*   **User-Friendly Interface:** Built with Bootstrap 5.3 for a responsive and intuitive design.
*   **GitHub API Integration:** Directly queries the GitHub REST API to retrieve user profile information.
*   **Account Creation Date:** Displays the `created_at` timestamp of a GitHub user's account in `YYYY-MM-DD UTC` format.
*   **Optional Authentication with Token:** Supports passing a GitHub Personal Access Token (PAT) via a URL query parameter (`?token=YOUR_TOKEN`) to benefit from higher API rate limits for authenticated requests.
*   **Error Handling:** Provides clear messages for invalid usernames, API rate limit issues, or other network/API errors.

## Usage

To use this application, simply follow these steps:

1.  **Open `index.html`:** Download the `index.html` file and open it in your web browser. You can do this by dragging the file into your browser, or serving it with a local web server (e.g., `python -m http.server` in the directory where `index.html` is located).
2.  **Enter GitHub Username:** Type the desired GitHub username into the "GitHub Username" input field.
3.  **Click "Get Creation Date":** The application will send a request to the GitHub API, and the creation date will be displayed below the form.

### Using a Personal Access Token (Optional)

If you encounter API rate limit issues (especially for unauthenticated requests, which are lower), or if you simply wish to make authenticated requests, you can provide a GitHub Personal Access Token.

To do this, append `?token=YOUR_PERSONAL_ACCESS_TOKEN` to the URL of the `index.html` page.

**Example:**
If your `index.html` is located at `http://localhost:8000/index.html`, you would access it like this:
`http://localhost:8000/index.html?token=ghp_YOUR_SUPER_SECRET_TOKEN_HERE`

**Important Security Note:** When using a Personal Access Token, ensure it has the minimum necessary scopes (typically none for public user data, but `public_repo` or others might be needed for more advanced queries). Never expose your PAT in publicly accessible code or commit it to version control. This implementation is for local testing and demonstration purposes; production applications should handle API keys more securely.

## Technical Details

*   **Frontend Technologies:** HTML5, CSS (Bootstrap 5.3), JavaScript.
*   **API Endpoint:** Utilizes the GitHub REST API `/users/{username}` endpoint.
*   **Date Formatting:** Dates are parsed from the API response and formatted to `YYYY-MM-DD UTC`.

## License

This project is open-sourced under the MIT License. The full license text can be found within the `<head>` section of the `index.html` file.