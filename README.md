# Maize App API

This is the backend API for the Maize application, built with Django and Django Rest Framework.

## Development

Details about setting up the development environment, running the application, and other development-related tasks would typically go here. (Currently, setup involves installing dependencies from `requirements.txt` and running the Django development server).

## Code Quality

The project uses several tools to maintain code quality:

*   **Black:** For automated code formatting, ensuring a consistent style across the codebase.
*   **Flake8:** For linting, to identify potential errors, style issues, and complexity problems. A `.flake8` configuration file is included to customize rules, such as line length (set to 88 characters) and specific errors to ignore (E203, W503 for compatibility with Black, and E501 for specific long lines in `app/app/settings.py` and `app/core/migrations/0001_initial.py` that were impractical to shorten further).

These tools are typically run as part of CI checks (e.g., GitHub Actions).

## Key Application Components

### Core App (`app/core`)

*   **Models (`models.py`):** Defines the custom `User` model, which uses email as the username, and a `UserManager` for user creation and management.
*   **Admin (`admin.py`):** Customizes the Django admin interface for the `User` model.
    *   Recent Refactoring: The `UserAdmin` configuration was updated to include the `name` field in the `fieldsets` for editing users. This ensures the `name` is visible and editable in the admin panel after a user is created, not just during creation.
*   **Tests (`tests/`):** Contains tests for models, admin interface, and management commands.

### User App (`app/user`)

*   **Views (`views.py`):** Provides API endpoints for user management:
    *   `CreateUserView`: For new user registration.
    *   `CreateTokenView`: For users to obtain an authentication token.
    *   `ManageUserView`: For authenticated users to retrieve and update their own profile information (name, email, password).
*   **Serializers (`serializers.py`):** Defines serializers for user data (`UserSerializer`) and authentication tokens (`AuthTokenSerializer`). These handle data validation, conversion, and password hashing.
*   **Review Note:** A recent review of the `user` app (views and serializers) concluded that it is well-structured, follows Django Rest Framework best practices, and did not require immediate refactoring.

## Note on Recent Activities (Test Coverage Efforts)

An effort was made to improve test coverage for `app/core/tests/test_models.py` and `app/user/tests/test_user_api.py`. New test cases were written to cover areas such as model field default values, validation rules, and more comprehensive API endpoint checks (e.g., missing fields, partial updates).

However, completion of this task was **blocked by persistent environment issues** within the development/testing sandbox. These issues included:
*   Inconsistent file system behavior observed by different file operation tools.
*   Difficulties in modifying `requirements.txt` to use `psycopg2-binary` instead of `psycopg2` (which failed to compile).
*   Consequently, the correct dependencies could not be reliably installed, preventing the successful execution of the test suite (including the newly added tests).

These environmental challenges need to be addressed to ensure tests can be run and validated.
