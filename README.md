# fastapi-auth-core
Basic, Reusable authentication module for FASTAPI

# FastAPI Auth Core

This project is a reusable backend module for handling user authentication and Role-Based Access Control (RBAC) in FastAPI. The goal is to create a secure and flexible foundation for any application that needs to manage users, roles, and permissions.

## Planned API Endpoints

The API will provide endpoints for authentication and for testing the auth system.

* `POST /auth/register`
    * Allows a new user to register for an account.
* `POST /auth/token`
    * Logs a user in. Takes an email and password, returns an access token and a refresh token.
* `POST /auth/refresh`
    * Takes a refresh token and returns a new access token.
* `GET /users/me`
    * A protected endpoint that returns the profile of the currently logged-in user.
* `GET /admin/dashboard`
    * A protected endpoint that demonstrates **role-based authorization**. Access requires the "Admin" role.
* `DELETE /articles/{article_id}`
    * A protected endpoint that demonstrates **permission-based authorization**. Access requires the `can_delete_articles` permission.

***
## RBAC Management Endpoints

These endpoints allow administrators to manage the roles and permissions system itself. Access requires a specific permission like `can_manage_rbac`.

* `GET /admin/permissions`
    * Lists all available permissions in the system.
* `POST /admin/users/{user_id}/roles`
    * Assigns a specific role to a user.
* `DELETE /admin/users/{user_id}/roles/{role_id}`
    * Removes a role from a user.
* `POST /admin/roles/{role_id}/permissions`
    * Grants a specific permission to a role.
* `DELETE /admin/roles/{role_id}/permissions/{permission_id}`
    * Revokes a permission from a role.

***
## Database Models

The database structure is designed for flexibility.

* **User**
    * `id`, `email`, `hashed_password`, `is_active`

* **Role**
    * `id`, `name` (e.g., "Admin"), `description`

* **Permission**
    * `id`, `name` (e.g., "can_delete_articles")

And two "many-to-many" link tables to connect them:

* A **User-Role** table to track which users have which roles.
* A **Role-Permission** table to track which permissions are granted to which roles.



# Running the Program
```shell
uvicorn main:app --reload
```