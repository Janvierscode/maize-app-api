MaizeDetect Community - Project Requirements Specification
Prepared by: Gemini (based on information from Janvier Iyakaremye)
Last Updated: April 18, 2025
Status: Requirements Specification (Expanded Scope)

1. Introduction
1.1 Purpose
This document specifies the requirements for the MaizeDetect Community project. It outlines the functional and non-functional requirements, system architecture, data model, and external interfaces necessary for the successful development and deployment of a lightweight, offline-capable mobile application and its supporting Django backend. The primary goal is to empower smallholder farmers with on-device AI for maize disease detection and facilitate robust community engagement through a feature-rich forum, including moderation, detailed disease information, notifications, and advanced search capabilities. The project also includes enhanced data backup options and integration with external services like weather data.

1.2 Project Scope
The expanded scope of the MaizeDetect Community project now includes:

Development of a cross-platform mobile application using Flutter.

Development of a RESTful API backend using Django and PostgreSQL.

Implementation of on-device AI for maize disease detection.

Implementation of an offline-first data storage and synchronization strategy.

Implementation of user authentication with Google Sign-In and manual registration.

Development of a comprehensive community forum with posting, replying, voting, advanced search, filtering, and sorting functionalities.

Implementation of a Moderator role for community content management.

Integration of detailed information about maize diseases within the app.

Implementation of push notifications for community activity.

Integration with external services, specifically a weather API relevant to maize growth and disease spread.

Implementation of both manual and automated scheduled data backup options to Google Drive.

Documentation of the API using Swagger.

The project excludes features such as:

Real-time chat (beyond the forum structure).

Integration with other cloud storage providers besides Google Drive.

In-app payments or monetization features.

Complex analytics or reporting features beyond basic data display.

1.3 Definitions, Acronyms, and Abbreviations
AI: Artificial Intelligence

API: Application Programming Interface

DRF: Django REST Framework

Flutter: UI toolkit for building natively compiled applications for mobile, web, and desktop from a single codebase.

GDPR: General Data Protection Regulation

JWT: JSON Web Token (Potential alternative to Token-based authentication)

MVP: Minimum Viable Product

PostgreSQL: Open-source relational database system.

REST: Representational State Transfer

SQLite: Serverless, self-contained, high-reliability, full-featured, public-domain, SQL database engine.

Swagger: An open-source framework backed by a large ecosystem of tools that helps design, build, document, and consume RESTful Web services.

UI: User Interface

UX: User Experience

1.4 References
Requirements Gathering Notes (Provided in prompt)

Django Documentation

Django REST Framework Documentation

Flutter Documentation

SQLite Documentation

PostgreSQL Documentation

Google Sign-In API Documentation

Google Drive API Documentation

Swagger Documentation

Chosen Weather API Documentation (To be determined)

1.5 Overview
The remainder of this document details the overall description of the product, including its functions, user characteristics, and constraints. It then specifies the detailed functional and non-functional requirements, external interfaces, data model, and API specifications, including the use of Swagger for documentation.

2. Overall Description
2.1 Product Perspective
MaizeDetect Community is a standalone mobile application with a supporting backend. It is the primary interface for users, operating independently offline and syncing data with the backend when connectivity is available. The backend serves as a central data repository, provides the API for synchronization and community features, manages user authentication, handles integrations, and facilitates automated backups.

2.2 Product Functions
The major functions of the MaizeDetect Community are:

On-Device Disease Detection: Allowing users to get instant AI diagnoses of maize diseases from photos, even offline.

Detailed Disease Information: Providing users with comprehensive information about detected diseases.

Community Engagement: Providing a feature-rich forum for users to share information, ask questions, and offer advice, with advanced search, filtering, and sorting.

Community Moderation: Allowing designated users to manage and curate community content.

Push Notifications: Alerting users to relevant activity within the community forum.

Data Synchronization: Seamlessly syncing user-generated data between the mobile device and the backend when online.

User Authentication: Providing a simple and low-friction sign-up process using Google or manual registration.

Data Backup: Allowing users to manually or automatically export their application data to their Google Drive account.

External Service Integration: Displaying relevant weather information alongside disease data and in the community context.

2.3 User Characteristics
The primary users of MaizeDetect Community are smallholder farmers, learners, and youth members who may have limited access to stable internet connectivity and may be using low-end smartphones. They require a simple, intuitive interface and reliable offline functionality. Basic literacy is assumed, but the interface should be as visual and user-friendly as possible. A secondary user type is the Moderator, who requires specific permissions and tools for content management.

2.4 Operating Environment
Mobile Application: Android and iOS smartphones (targeting a range of device capabilities, including low-end devices). Requires access to the device's camera, local storage, and notification capabilities. Requires internet connectivity for synchronization, initial setup, and receiving push notifications.

Backend: Server environment capable of running Docker containers, supporting Django, PostgreSQL, internet connectivity for mobile app communication, external API calls (e.g., weather), and potentially external AI model updates (though initial model is on-device).

2.5 Design and Implementation Constraints
Offline-First Capability: The application must be fully functional for core features (disease detection, viewing cached community content and detailed disease info) without an internet connection.

Performance on Low-End Devices: The AI inference and overall application responsiveness must be fast on less powerful smartphones (inference < 2 seconds).

Minimal Sign-Up Friction: The registration process should be quick and simple, mimicking the WhatsApp-style onboarding.

On-Device AI Model: The AI model for disease detection must run locally on the device.

Google Drive Integration: Backup functionality is limited to manual and automated scheduled export to the user's own Google Drive.

Security and Data Privacy: User data must be handled securely, with encrypted communication and consideration for anonymous usage and GDPR alignment.

API Documentation: The backend API must be documented using Swagger.

2.6 Assumptions and Dependencies
Users have access to a smartphone with a working camera.

Users have a Google account if they choose the Google Sign-In or Google Drive backup options.

Users have sufficient local storage space on their device for the app and data caching.

A pre-trained, optimized AI model for maize disease detection suitable for on-device inference will be provided or integrated.

Reliable internet connectivity is available periodically for data synchronization, receiving push notifications, and automated backups.

Google APIs for Sign-In and Drive are available and accessible.

A suitable weather API with relevant data for maize growth is available and accessible.

3. Specific Requirements
3.1 Functional Requirements
3.1.1 User Authentication and Identity
FR-AUTH-1: The system shall allow users to register using their Google account (one-tap sign-in).

FR-AUTH-2: The system shall retrieve the user's name, email, and profile photo (if available) from their Google account upon successful sign-in.

FR-AUTH-3: The system shall allow users to register manually by providing their name and email address.

FR-AUTH-4: The system shall allow users to optionally provide a profile photo during manual sign-up.

FR-AUTH-5: The system shall perform a one-time registration process for each user.

FR-AUTH-6: The system shall persist the user's authentication token locally on the device after the initial login.

FR-AUTH-7: The system shall automatically log in the user on subsequent app launches using the stored token.

FR-AUTH-8: The system shall provide an option for users to post content anonymously in the community forum.

3.1.2 Disease Detection
FR-DETECT-1: The system shall allow users to capture a photo of a maize leaf using the device's camera.

FR-DETECT-2: The system shall allow users to upload an existing photo of a maize leaf from their device's gallery.

FR-DETECT-3: The system shall perform AI inference on the captured or uploaded photo using the local model.

FR-DETECT-4: The system shall display the instant AI diagnosis result to the user on the device.

FR-DETECT-5: The diagnosis result shall include the detected disease type and a confidence score.

FR-DETECT-6: The system shall allow users to optionally share their detection result (photo and diagnosis) with the community forum.

FR-DETECT-7: The system shall store detection results locally on the device.

FR-DETECT-8: The system shall sync local detection results to the backend when an internet connection is available.

3.1.3 Detailed Disease Information
FR-INFO-1: The system shall store detailed information for each detectable maize disease, including:

Symptoms

Causes (e.g., pathogens, environmental factors)

Prevention methods

Treatment options

Relevant images or diagrams

FR-INFO-2: Users shall be able to access this detailed information directly from the disease detection result screen.

FR-INFO-3: Users shall be able to browse a list of all known maize diseases supported by the app and view their detailed information.

FR-INFO-4: Detailed disease information shall be available offline once initially downloaded or included in the app bundle.

3.1.4 Community Forum
FR-COMM-1: The system shall display a feed of community posts.

FR-COMM-2: The system shall allow users to view the details of a specific post, including replies.

FR-COMM-3: The system shall allow users to create a new post in the forum.

FR-COMM-4: Posts can include text and optionally a shared disease detection result (photo and diagnosis).

FR-COMM-5: Posts shall be tagged by disease type (if related to a detection or explicitly specified).

FR-COMM-6: The system shall allow users to reply to existing posts.

FR-COMM-7: Replies shall be displayed in a threaded manner under the corresponding post.

FR-COMM-8: The system shall allow users to upvote or downvote posts.

FR-COMM-9: The system shall allow users to upvote or downvote replies.

FR-COMM-10: Each user shall be limited to one vote (up or down) per post or reply.

FR-COMM-11: The system shall display the net vote count for each post and reply.

FR-COMM-12: Community data (posts, replies, votes) shall be cached locally for offline viewing.

FR-COMM-13: The system shall provide a search functionality to find posts and replies based on keywords or phrases.

FR-COMM-14: The system shall allow users to filter community posts by disease type, user (if not anonymous), or other relevant criteria (e.g., posts with detections).

FR-COMM-15: The system shall allow users to view posts sorted by different criteria (e.g., latest activity, creation date, most voted, number of replies).

FR-COMM-16: The system shall allow users to "follow" specific posts to receive notifications about new replies.

3.1.5 Community Moderation
FR-MOD-1: The system shall allow designated users to have a "Moderator" role with specific backend permissions.

FR-MOD-2: Moderators shall be able to view all community posts and replies, including those that may have been flagged.

FR-MOD-3: Moderators shall be able to delete inappropriate posts from the community forum.

FR-MOD-4: Moderators shall be able to delete inappropriate replies from the community forum.

FR-MOD-5: The system shall provide a mechanism for standard users to flag posts or replies as inappropriate.

FR-MOD-6: The system shall provide a moderator interface (potentially within the app or a separate web view) to view and action flagged content.

3.1.6 Push Notifications
FR-NOTIF-1: The backend shall send push notifications to users when someone replies to a post they created.

FR-NOTIF-2: The backend shall send push notifications to users when someone replies to a post they have previously replied to (if they have notifications enabled for that thread).

FR-NOTIF-3: The backend shall send push notifications to users when there is activity on a post they are "following".

FR-NOTIF-4: The mobile application shall provide settings for users to manage their notification preferences (e.g., enable/disable notifications for replies to my posts, replies to threads I've participated in, followed posts).

3.1.7 Data Sync and Storage
FR-SYNC-1: The mobile application shall store all user-generated data (detections, posts, replies, votes, notification preferences, backup settings) locally using SQLite.

FR-SYNC-2: The system shall mark local data entries with a synced status (e.g., boolean flag) and a last_updated_at timestamp.

FR-SYNC-3: The mobile application shall initiate a synchronization process with the backend when an internet connection is detected.

FR-SYNC-4: The sync process shall upload unsynced local data to the backend via the REST API.

FR-SYNC-5: The sync process shall download new or updated data from the backend to the local database.

FR-SYNC-6: The sync process shall be secure and authenticated using the user's token.

FR-SYNC-7: Sync actions that fail due to network issues or other errors shall be queued and retried automatically.

FR-SYNC-8: Conflict resolution during sync shall follow a "latest-write-wins" strategy based on the last_updated_at timestamp for each record.

3.1.8 Data Backup
FR-BACKUP-1: The system shall provide a user interface option to manually trigger a data backup to Google Drive.

FR-BACKUP-2: The backup shall export a snapshot of the user's application data (detections, posts, replies, votes, notification preferences, backup settings) in a structured format (e.g., JSON or SQLite file).

FR-BACKUP-3: The system shall upload the exported data file to the user's linked Google Drive account.

FR-BACKUP-4: The backup process shall require the user's explicit permission to access their Google Drive.

FR-BACKUP-5: The system shall allow users to configure automated scheduled backups of their data to Google Drive (e.g., daily, weekly, monthly).

FR-BACKUP-6: The mobile application shall provide a user interface to manage automated backup settings (schedule, enable/disable).

FR-BACKUP-7: The system shall notify the user within the app if an automated backup fails.

FR-BACKUP-8: The system shall handle potential issues with Google Drive integration (e.g., account disconnected, storage full).

3.1.9 External Service Integration (Weather)
FR-INTEG-1: The backend shall integrate with a chosen weather API to fetch relevant weather information for user-specified locations (e.g., location associated with a detection or user's general location).

FR-INTEG-2: Relevant weather information (e.g., temperature, humidity, recent rainfall) shall be displayed alongside disease detection results.

FR-INTEG-3: Relevant weather information may be displayed in the community forum context if a post is tagged with a location or disease type influenced by weather.

FR-INTEG-4: Weather data fetched from the API shall be cached locally on the mobile device for offline viewing for a limited time.

3.2 Non-Functional Requirements
NFR-PERF-1: The AI inference for disease detection shall complete within 2 seconds on target low-end smartphones.

NFR-PERF-2: The mobile application shall remain responsive during offline use, synchronization, and when displaying detailed information or community content.

NFR-PERF-3: Search and filtering operations within the community forum should be performant, even with a large number of posts.

NFR-SEC-1: Communication between the mobile application and the backend shall be encrypted (e.g., using HTTPS).

NFR-SEC-2: User authentication tokens shall be stored securely on the device.

NFR-SEC-3: User data stored locally and on the backend shall be protected against unauthorized access.

NFR-SEC-4: The system shall comply with relevant data privacy regulations (e.g., GDPR), including supporting anonymous usage and providing options for data export/deletion.

NFR-SCAL-1: The backend infrastructure shall be designed to handle thousands of concurrent users and a growing volume of data records, including detections, posts, replies, and votes.

NFR-SCAL-2: The database schema and queries should be optimized for performance under load.

NFR-OFFLINE-1: Core functionalities (disease detection, viewing cached community content, viewing detailed disease info) shall be fully available when the device is offline.

NFR-OFFLINE-2: The sync mechanism shall reliably queue and retry failed synchronization attempts, ensuring eventual consistency.

NFR-USABILITY-1: The mobile application shall have an intuitive and easy-to-navigate user interface, minimizing friction for the target user group.

NFR-USABILITY-2: The process for configuring and managing automated backups should be clear and simple.

NFR-MAINTAIN-1: The codebase for both the mobile application and the backend shall be well-structured, documented, and easy to maintain and extend.

NFR-MAINTAIN-2: The API endpoints shall be clearly defined and documented using Swagger.

NFR-PORT-1: The mobile application, being developed with Flutter, shall be deployable on both Android and iOS platforms from a single codebase.

NFR-RELIABILITY-1: The automated backup process should be reliable and provide clear feedback to the user on its status.

3.3 External Interface Requirements
3.3.1 User Interfaces
The mobile application shall have a user-friendly interface designed for small screens and touch interaction.

Key screens will include: Onboarding/Registration, Disease Detection (camera/gallery interface, results display, detailed info access), Community Feed (with search, filter, sort options), Post/Reply Creation, Settings (including backup and notification options), Moderator Interface (if applicable within the app).

UI flows will be detailed in separate wireframes and design specifications.

3.3.2 Hardware Interfaces
Camera: The mobile application requires access to the device's camera to capture photos for disease detection.

Storage: The mobile application requires access to the device's local storage to store the application data (SQLite database), cached content, and potentially the AI model file.

Notification Capabilities: The mobile application requires access to the device's notification system to display push notifications.

3.3.3 Software Interfaces
Operating System: The mobile application will interface with the Android and iOS operating systems.

Google APIs: The application will interface with Google Sign-In API for authentication and Google Drive API for manual and automated data backup.

AI Model Integration: The mobile application will integrate with the chosen on-device AI inference engine and the pre-trained maize disease detection model.

Weather API: The backend will interface with a chosen external Weather API to fetch relevant weather data.

Push Notification Service: The backend will integrate with a push notification service (e.g., Firebase Cloud Messaging) to send notifications to mobile devices.

3.3.4 Communication Interfaces
The mobile application will communicate with the Django backend via a RESTful API over HTTPS.

The backend will communicate with the Weather API over HTTPS.

The backend will communicate with the push notification service API.

The application will use standard network protocols for internet connectivity.

4. Data Model
This section describes the main entities and their relationships within the MaizeDetect Community system.

User:

id (Primary Key)

google_id (String, Nullable - if using Google Sign-In)

email (String, Unique)

name (String)

profile_photo_url (String, Nullable)

auth_token (String - for API authentication)

is_anonymous (Boolean - indicates if the user is currently posting anonymously)

role (String - e.g., 'standard', 'moderator')

notification_settings (JSON Field - stores user notification preferences)

backup_settings (JSON Field - stores automated backup schedule and preferences)

created_at (Timestamp)

updated_at (Timestamp)

Disease:

id (Primary Key)

name (String, Unique)

description (Text - detailed info)

symptoms (Text)

causes (Text)

prevention (Text)

treatment (Text)

image_urls (JSON Field - URLs of relevant images)

created_at (Timestamp)

updated_at (Timestamp)

Disease Detection:

id (Primary Key)

user (Foreign Key to User)

image_url (String - URL of the stored image, potentially local path initially)

detected_disease (Foreign Key to Disease)

confidence_score (Float)

location (JSON Field, Nullable - stores geographical coordinates if available)

weather_data (JSON Field, Nullable - cached weather data at time of detection)

synced (Boolean - for mobile app tracking)

created_at (Timestamp)

updated_at (Timestamp)

Post:

id (Primary Key)

user (Foreign Key to User)

content (Text)

detection (Foreign Key to Disease Detection, Nullable - if the post is not linked to a specific detection)

disease_tag (Foreign Key to Disease, Nullable - manually added tag)

is_anonymous (Boolean - reflects the user's is_anonymous status at the time of posting)

synced (Boolean - for mobile app tracking)

is_flagged (Boolean - indicates if the post has been flagged)

created_at (Timestamp)

updated_at (Timestamp)

Reply:

id (Primary Key)

user (Foreign Key to User)

post (Foreign Key to Post)

content (Text)

is_anonymous (Boolean - reflects the user's is_anonymous status at the time of replying)

synced (Boolean - for mobile app tracking)

is_flagged (Boolean - indicates if the reply has been flagged)

created_at (Timestamp)

updated_at (Timestamp)

Vote:

id (Primary Key)

user (Foreign Key to User)

post (Foreign Key to Post, Nullable)

reply (Foreign Key to Reply, Nullable)

vote_type (Integer - e.g., +1 for upvote, -1 for downvote)

synced (Boolean - for mobile app tracking)

created_at (Timestamp)

updated_at (Timestamp)

(Constraint: A vote must be linked to either a Post or a Reply, but not both)

(Constraint: A user can only have one vote per Post or Reply)

Flag:

id (Primary Key)

user (Foreign Key to User - the user who flagged)

post (Foreign Key to Post, Nullable - the flagged post)

reply (Foreign Key to Reply, Nullable - the flagged reply)

reason (Text, Nullable - reason for flagging)

resolved (Boolean - indicates if a moderator has reviewed the flag)

resolved_by (Foreign Key to User, Nullable - the moderator who resolved it)

resolved_at (Timestamp, Nullable)

created_at (Timestamp)

(Constraint: A flag must be linked to either a Post or a Reply, but not both)

5. API Specification
The backend will expose a comprehensive RESTful API using Django REST Framework. Authentication will be token-based (or potentially JWT). The API endpoints will be documented using Swagger.

POST /api/register/

Description: Registers a new user.

Request Body: User details (name, email, optional password for manual, or Google token).

Response Body: User details and authentication token.

Authentication: None (for manual registration), handled by Google OAuth for Google Sign-In.

POST /api/login/

Description: Authenticates an existing user.

Request Body: User credentials (email/password for manual) or Google token.

Response Body: User details and authentication token.

Authentication: None.

POST /api/detections/

Description: Uploads a new disease detection result.

Request Body: Detection details (user ID, image data/URL, detected disease ID, confidence score, optional location).

Response Body: Created detection object.

Authentication: Token required.

GET /api/detections/

Description: Retrieves a user's detection history.

Query Parameters: Optional filters (e.g., by date, disease ID).

Response Body: List of detection objects.

Authentication: Token required.

GET /api/diseases/

Description: Lists all known maize diseases with detailed information.

Response Body: List of Disease objects.

Authentication: Optional.

GET /api/diseases/{disease_id}/

Description: Retrieves detailed information for a specific disease.

Response Body: Disease object.

Authentication: Optional.

GET /api/posts/

Description: Lists community posts with options for searching, filtering, and sorting.

Query Parameters:

search: Keyword for searching content.

disease_id: Filter by disease tag.

user_id: Filter by user (if not anonymous).

has_detection: Boolean filter for posts with linked detections.

sort_by: Field to sort by (e.g., created_at, vote_count, reply_count).

order: Sort order (asc, desc).

Response Body: Paginated list of post objects, including vote counts and potentially initial replies.

Authentication: Optional (can view public posts without auth).

POST /api/posts/

Description: Creates a new community post.

Request Body: Post details (user ID, content, optional detection ID, optional disease ID tag, is_anonymous flag).

Response Body: Created post object.

Authentication: Token required.

GET /api/posts/{post_id}/replies/

Description: Lists replies for a specific post.

Response Body: List of reply objects.

Authentication: Optional (can view replies for public posts without auth).

POST /api/posts/{post_id}/replies/

Description: Creates a new reply for a post.

Request Body: Reply details (user ID, post ID, content, is_anonymous flag).

Response Body: Created reply object.

Authentication: Token required.

POST /api/votes/

Description: Submits a vote for a post or reply.

Request Body: Vote details (user ID, post ID or reply ID, vote type).

Response Body: Updated vote counts for the item.

Authentication: Token required.

DELETE /api/votes/{vote_id}/

Description: Removes a user's vote.

Authentication: Token required.

POST /api/flags/

Description: Flags a post or reply as inappropriate.

Request Body: Flag details (user ID, post ID or reply ID, optional reason).

Response Body: Created flag object.

Authentication: Token required.

GET /api/flags/

Description: Lists flagged content (Moderator only).

Query Parameters: Optional filters (e.g., resolved=false).

Response Body: List of Flag objects.

Authentication: Token required (Moderator role).

PATCH /api/flags/{flag_id}/

Description: Updates a flag's status (e.g., marks as resolved) (Moderator only).

Request Body: Update details (e.g., resolved=true, resolved_by).

Response Body: Updated Flag object.

Authentication: Token required (Moderator role).

DELETE /api/posts/{post_id}/

Description: Deletes a post (Moderator only).

Authentication: Token required (Moderator role).

DELETE /api/replies/{reply_id}/

Description: Deletes a reply (Moderator only).

Authentication: Token required (Moderator role).

POST /api/users/me/notification_settings/

Description: Updates the current user's notification settings.

Request Body: JSON containing notification preferences.

Response Body: Updated user object with notification settings.

Authentication: Token required.

GET /api/users/me/notification_settings/

Description: Retrieves the current user's notification settings.

Response Body: JSON containing notification preferences.

Authentication: Token required.

POST /api/users/me/backup_settings/

Description: Updates the current user's automated backup settings.

Request Body: JSON containing backup schedule and preferences.

Response Body: Updated user object with backup settings.

Authentication: Token required.

GET /api/users/me/backup_settings/

Description: Retrieves the current user's automated backup settings.

Response Body: JSON containing backup schedule and preferences.

Authentication: Token required.

POST /api/users/me/backup/manual/

Description: Triggers a manual data backup to Google Drive.

Authentication: Token required.

GET /api/weather/

Description: Retrieves weather information for a given location.

Query Parameters: latitude, longitude.

Response Body: Weather data fetched from the external API.

Authentication: Optional (weather data might be public or tied to detection).

Error Handling: The API should return standard HTTP status codes (e.g., 200 OK, 201 Created, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 500 Internal Server Error) with informative error messages in the response body.

Swagger Documentation: The API endpoints, request/response formats, and authentication requirements will be documented using Swagger. This documentation will be accessible via a dedicated endpoint on the backend (e.g., /swagger-ui/).

6. System Architecture
The MaizeDetect Community system follows a client-server architecture:

Mobile Application (Flutter): The frontend, running on Android and iOS devices. Handles the user interface, on-device AI inference, local data storage (SQLite), initiates synchronization with the backend, manages local notification settings, and interacts with Google Drive for backups.

Django Backend: The server-side application, providing the RESTful API, managing the PostgreSQL database, handling user authentication and authorization (including moderator roles), managing notification preferences, interacting with the Weather API, and coordinating automated backups with Google Drive.

PostgreSQL Database: The central relational database storing all synchronized user data, community content, user information, disease details, flags, and settings.

Google Drive: Used as an external service for both manual and automated data backups initiated via the backend or mobile app.

Weather API: An external service providing weather data, consumed by the Django backend.

Push Notification Service: An external service (e.g., Firebase Cloud Messaging) used by the backend to send notifications to mobile devices.

The mobile application communicates with the Django backend via secure API calls. The backend interacts with the PostgreSQL database, the Weather API, and the Push Notification Service. The mobile app or backend interacts with Google Drive for backups.

7. Appendix
7.1 User Journeys
(As provided in the prompt, these journeys now incorporate the expanded features)

First-time user: Opens app → Sees onboarding → Signs up (Google or manual) → Ready to use

Detect disease: Tap detect → Upload or take photo → Result appears instantly → View detailed disease info → Option to share with community (potentially including weather data)

Community: View posts (with search/filter/sort options) → View detailed post (including replies and weather data if linked) → Reply to a thread or ask a question → Vote on helpful posts → Flag inappropriate content → Follow a post

Moderation: Access moderator interface → View flagged content → Delete inappropriate posts/replies

Backup: Go to settings → Tap "Backup to Drive" (manual) OR Configure automated backup schedule

Notifications: Receive push notifications for community activity → Go to settings to manage notification preferences

7.2 UI Flows
UI flows and wireframes will be developed in a separate document to detail the user interface interactions and screen layouts for all features, including the newly added ones.