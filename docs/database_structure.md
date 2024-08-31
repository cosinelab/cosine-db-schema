### 1. Users

**Description**: Stores information about users.

| Column Name     | Data Type     | Constraints                              | Description                                         |
| --------------- | ------------- | ---------------------------------------- | --------------------------------------------------- |
| `user_id`       | `INT`         | `PRIMARY KEY`, `AUTO_INCREMENT`          | Unique identifier for each user.                    |
| `username`      | `VARCHAR(255)`| `UNIQUE`, `NOT NULL`                     | User’s unique username.                             |
| `email`         | `VARCHAR(255)`| `UNIQUE`, `NOT NULL`                     | User’s email address.                               |
| `password_hash` | `VARCHAR(255)`| `NOT NULL`                               | Hashed password for authentication.                 |
| `full_name`     | `VARCHAR(255)`| `NULL`                                   | Full name of the user.                              |
| `affiliation`   | `VARCHAR(255)`| `NULL`                                   | Affiliation or institution of the user.             |
| `role`          | `ENUM('Scientist', 'Admin', 'Guest')` | `NOT NULL` | Role assigned to the user.                          |
| `created_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`, `NOT NULL`  | Timestamp of when the user was created.             |
| `updated_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`, `NOT NULL`, `ON UPDATE CURRENT_TIMESTAMP` | Timestamp of the last update to the user's profile. |

### 2. Projects

**Description**: Stores project information and metadata.

| Column Name     | Data Type     | Constraints                              | Description                                         |
| --------------- | ------------- | ---------------------------------------- | --------------------------------------------------- |
| `project_id`    | `INT`         | `PRIMARY KEY`, `AUTO_INCREMENT`          | Unique identifier for each project.                 |
| `project_name`  | `VARCHAR(255)`| `NOT NULL`                               | Name of the project.                                |
| `description`   | `TEXT`        | `NULL`                                   | Detailed description of the project.                |
| `owner_id`      | `INT`         | `FOREIGN KEY` (references `Users(user_id)`), `NOT NULL` | ID of the user who owns the project. |
| `created_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`, `NOT NULL`  | Timestamp of when the project was created.          |
| `updated_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`, `NOT NULL`, `ON UPDATE CURRENT_TIMESTAMP` | Timestamp of the last update to the project.        |

### 3. Collaborators

**Description**: Manages the relationship between users and projects.

| Column Name     | Data Type     | Constraints                              | Description                                         |
| --------------- | ------------- | ---------------------------------------- | --------------------------------------------------- |
| `collaborator_id`| `INT`        | `PRIMARY KEY`, `AUTO_INCREMENT`          | Unique identifier for each collaborator entry.       |
| `project_id`    | `INT`         | `FOREIGN KEY` (references `Projects(project_id)`), `NOT NULL` | ID of the associated project. |
| `user_id`       | `INT`         | `FOREIGN KEY` (references `Users(user_id)`), `NOT NULL` | ID of the user collaborating on the project. |
| `role`          | `ENUM('Viewer', 'Editor', 'Owner')` | `NOT NULL` | Role of the user within the project.                |
| `added_at`      | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`, `NOT NULL`  | Timestamp of when the user was added as a collaborator. |

### 4. Notifications

**Description**: Stores notifications for users.

| Column Name     | Data Type     | Constraints                              | Description                                         |
| --------------- | ------------- | ---------------------------------------- | --------------------------------------------------- |
| `notification_id`| `INT`        | `PRIMARY KEY`, `AUTO_INCREMENT`          | Unique identifier for each notification.            |
| `user_id`       | `INT`         | `FOREIGN KEY` (references `Users(user_id)`), `NOT NULL` | ID of the user receiving the notification. |
| `message`       | `TEXT`        | `NOT NULL`                               | The notification message content.                   |
| `is_read`       | `BOOLEAN`     | `DEFAULT FALSE`, `NOT NULL`              | Status indicating whether the notification has been read. |
| `created_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`, `NOT NULL`  | Timestamp of when the notification was created.     |
