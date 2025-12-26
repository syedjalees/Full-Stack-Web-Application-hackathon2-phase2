# Phase II: Full-Stack Web App Requirements

## 1. Project Overview

This document outlines the requirements for a full-stack web application that allows users to manage their tasks. The application will feature a modern, responsive user interface and a secure, scalable backend.

## 2. Core Features

### 2.1. Authentication
- User Sign up/Sign in using Email/Password (via Better Auth).
- User Logout.
- Protected Routes (cannot view dashboard without login).

### 2.2. Task Management (CRUD)
- **Create:** User can add a task (Title required, Description optional).
- **Read:** View a list of tasks. **Crucial:** User sees ONLY their own tasks.
- **Update:** Edit task details.
- **Delete:** Remove a task.
- **Complete:** Toggle completion status.

### 2.3. UI/UX
- A landing page for non-logged-in users.
- A Dashboard for logged-in users.
- Use a Toaster for success/error notifications.
- Loading states (skeletons) while fetching data.

## 3. User Journeys

### 3.1. New User Registration
1.  A new user visits the landing page and clicks the "Sign Up" button.
2.  They are presented with a form to enter their email and password.
3.  Upon successful submission, their account is created, they are logged in, and redirected to their personal dashboard.
4.  A success notification ("Account created successfully!") is displayed.

### 3.2. Existing User Login
1.  An existing user visits the landing page and clicks the "Sign In" button.
2.  They enter their email and password.
3.  Upon successful authentication, they are redirected to their dashboard.
4.  A success notification ("Logged in successfully!") is displayed.

### 3.3. User Logout
1.  A logged-in user clicks the "Logout" button.
2.  Their session is terminated, and they are redirected to the landing page.
3.  A success notification ("Logged out successfully!") is displayed.

### 3.4. Task Creation
1.  A logged-in user on their dashboard clicks the "Add Task" button.
2.  A form or modal appears, prompting for a task title (required) and description (optional).
3.  After submitting the form, the new task immediately appears in their task list.
4.  A success notification ("Task created!") is displayed.

### 3.5. Task Viewing & Data Isolation
1.  Upon logging in, the user is taken to the dashboard.
2.  While the tasks are being fetched, a loading state (e.g., skeleton UI) is shown.
3.  The dashboard then displays a list of tasks that belong exclusively to the logged-in user.

### 3.6. Task Update
1.  The user clicks an "Edit" icon or button on a specific task.
2.  A form or modal appears pre-filled with the task's current title and description.
3.  The user modifies the details and saves the changes.
4.  The task list updates to show the new information.
5.  A success notification ("Task updated!") is displayed.

### 3.7. Task Completion
1.  The user clicks a checkbox or toggle next to a task.
2.  The task's UI changes to reflect its completed status (e.g., strikethrough text).
3.  The completion status is persisted in the database.

### 3.8. Task Deletion
1.  The user clicks a "Delete" icon or button on a specific task.
2.  A confirmation dialog appears to prevent accidental deletion.
3.  Upon confirmation, the task is permanently removed from the list and the database.
4.  A success notification ("Task deleted!") is displayed.

### 3.9. Unauthorized Access
1.  A user who is not logged in attempts to navigate directly to the `/dashboard` URL.
2.  The application redirects them to the sign-in page.

## 4. Acceptance Criteria

### 4.1. Authentication
- [ ] Users can create a new account using an email and password.
- [ ] Users can sign in with valid credentials.
- [ ] Users receive a clear error message for failed sign-in attempts.
- [ ] Users can log out, which clears their session.
- [ ] Dashboard and other data-sensitive routes are protected and redirect unauthenticated users to the login page.
- [ ] A JWT is issued upon successful login and stored securely on the client.
- [ ] The JWT is sent in the authorization header for all subsequent API requests.

### 4.2. Task Management
- [ ] A logged-in user can create a new task with at least a title.
- [ ] A logged-in user can view a list of all their tasks.
- [ ] The task list **must not** display tasks from other users.
- [ ] A logged-in user can edit the title and description of their own tasks.
- [ ] A logged-in user can toggle the completion status of a task.
- [ ] A logged-in user can delete their own tasks, with a confirmation step.

### 4.3. UI/UX
- [ ] A visually distinct landing page exists for unauthenticated users.
- [ ] A dashboard page is the primary view for authenticated users.
- [ ] Non-blocking toaster notifications are used for success and error feedback.
- [ ] Skeleton screens or equivalent loading indicators are displayed when data is being fetched.
- [ ] The application is responsive and provides a good user experience on both mobile and desktop viewports.

## 5. Database Schema Constraints

-   **`Users` Table:**
    -   Must be compatible with the authentication provider.
    -   Must contain a unique user identifier (e.g., `id`).
-   **`Tasks` Table:**
    -   `id`: Primary Key.
    -   `title`: String, Not Null.
    -   `description`: String, Nullable.
    -   `is_completed`: Boolean, default `false`.
    -   `user_id`: Foreign Key that references the `id` in the `Users` table. This is **critical** for data isolation.