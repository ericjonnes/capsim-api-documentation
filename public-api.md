# Public API

## Authentication

### POST /api/v1/auth/login

Authenticates a user and returns their login information.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| Username | String | Users username |
| Password | String | Users password |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| token | string | Tells system login was successful |
| userID | integer | User identifier |
| Role | enum[“student”, “faculty”] | States user role |

**Example URL**

- api.example.com/api/v1/auth/login

## Student — Projects

### GET /api/v1/projects

Lists available projects.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| Token | string | Identifies the logged-in student |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Unique project identifier |
| projectName | string | Name of project |
| Description | string | Short project description |
| Status | string | Current project status |

**Example URL**

- api.example.com/api/v1/projects

### GET /api/v1/projects/{projectId}

Retrieves the requested project information.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Unique project identifier |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| projectID | int | Unique project identifier |
| projectName | string | Name of project |
| Description | string | Project description |
| startDate | date time | Date project becomes available |
| endDate | date time | Date project availability ends |
| Status | string | Current project status |

**Example URL**

- api.example.com/api/v1/projects/12

## Student — Inbox and Responses

### GET /api/v1/projects/{projectId}/messages

Lists available messages for a student project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Project containing the messages |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | int | Unique message identifier |
| Subject | string | Message title or subject |
| senderName | string | Name of sending character |
| messageType | enum(email, instant_message) | Type of message |
| isRead | boolean | Whether the student has opened the message |

**Example URL**

- api.example.com/api/v1/projects/12/messages

### GET /api/v1/messages/{messageId}

Retrieves the contents and response options for a message.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | int | Identifies the message being opened |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | int | Message identifier |
| scenarioId | int | Scenario associated with the message |
| senderName | string | Character sending the message |
| Subject | string | Message subject |
| Body | string | Full message content |
| Options | array[object] | Available responses the student can select |
| optionId | int | Unique option identifier |
| responseText | string | Text of the response option |

**Example URL**

- api.example.com/api/v1/messages/25

### POST /api/v1/messages/{messageId}/responses

Submits the student’s selected response to a message.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | int | Message the student is responding to |
| optionId | int | Selected response option |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| submissionId | int | Identifier of the saved response |
| messageId | int | Message that was answered |
| selectedOptionId | int | Selected answer |
| submittedAt | date time | Time the answer was submitted |
| Success | boolean | Indicates whether the submission succeeded |

**Example URL**

- api.example.com/api/v1/messages/25/responses

### GET /api/v1/messages/{messageId}/attachments

Lists resources attached to a message.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | int | Message containing the attachements |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| Attachments | array[object] | Files attached to the message |
| reourceId | int | Resource identifier |
| fileType | string | File format |
| fileName | string | Name of file |
| downloadUrl | string | Authorized URL used to access the attachment |

**Example URL**

- api.example.com/api/v1/messages/25/attachments

### GET /api/v1/projects/{projectId}/sent

Retrieves messages the student has already answered.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Project containing the sent messages |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| sentMessages | array[object] | Messages the student has already answered |
| messageId | int | Message identifier |
| Subject | string | Message subject |
| selectedOptionId | int | Response selected by the student |
| submittedAt | datetime | Time the response was submitted |

**Example URL**

- api.example.com/api/v1/projects/12/sent

## Student — Resources

### GET /api/v1/projects/{projectId}/resources

Lists available projects.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Project containing the drive resources |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| Resources | array[object] | Available project files |
| resourceId | int | Resource identifier |
| resourceName | string | Name of resource |
| Description | string | Description of its contents |
| fileType | string | Type of resource |

**Example URL**

- api.example.com/api/v1/projects/12/resources

### GET /api/v1/resources/{resourceId}

Retrieves the requested resource information.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| resourceId | int | Identifies the resource being opened |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| resourceId | int | Resource identifier |
| resourceName | string | Name of resource |
| Description | string | Resource description |
| downloadUrl | string | Authorized URl used to access the resource |

**Example URL**

- api.example.com/api/v1/resources/8

## Student — Instant Messages

### GET /api/v1/projects/{projectId}/threads

Lists available instant-message threads for a project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Project containing the instant-message threads |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| Threads | array[object] | List of available message threads |
| threadId | int | Unique thread identifier |
| characterName | string | Character associated with the conversation |
| lastMessage | string | Most recent message preview |
| lastUpdate | date time | Time of the recent message |

**Example URL**

- api.example.com/api/v1/projects/12/threads

### GET /api/v1/threads/{threadId}/messages

Lists messages within a conversation.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| threadId | identifies the conversation | — |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| Messages | array[object] | Messages in the conversation |
| messageId | int | Unique message identifier |
| senderId | int | Identifier of the sender |
| Content | string | Message content |
| sentAt | date time | Time the message was sent |

**Example URL**

- api.example.com/api/v1/threads/6/messages

### POST /api/v1/threads/{threadId}/messages

Sends a new message within a conversation.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| threadId | int | Conversation receiving the message |
| Content | string | Message being sent |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | int | Identifier of the created message |
| threadId | int | Conversation identifier |
| sentAt | date time | Time the message was sent |
| Success | boolean | Indicates whether the message was saved |

**Example URL**

- api.example.com/api/v1/threads/6/messages

## Student — Results

### GET /api/v1/projects/{projectId}/results

Retrieves the logged-in student’s project results and feedback.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Project containing the student’s results |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| reportId | int | Unique report identifier |
| totalScore | int | Students overall score |
| skillScores | object | Scores for communication, leadership, integrity, knowledge, and creativity |
| Feedback | string | Feedback associated with the student’s performance |
| completedAt | date time | Time the assessment was completed |

**Example URL**

- api.example.com/api/v1/projects/12/results

## Faculty — Projects

### GET /api/v1/faculty/projects

Lists available projects.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| authenticationToken | String | Identifies the faculty user |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| Projects | array[object] | Faculty user's projects, each containing |
| projectId | int | Project identifier |
| projectName | string | Project name |
| Status | string | Current project status |

**Example URL**

- api.example.com/api/v1/faculty/projects

### POST /api/v1/faculty/projects

Creates a new project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectName | string | Name of project Description Description of project Output |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | new project identifier |
| projectName | string | Name of created project |
| Success | boolean | Whether project was created |

**Example URL**

- api.example.com/api/v1/faculty/projects

### GET /api/v1/faculty/projects/{projectId}

Retrieves the requested project information.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Project being retrieved |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | int | Project identifier |
| projectName | String | Project name. |
| description | String | Project description. |
| status | String | Current project status. |
| startDate | Datetime | Project start date. |
| endDate | Datetime | Project end date. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12

### PATCH /api/v1/faculty/projects/{projectId}

Updates the specified project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project to update. |
| projectName | String (optional) | Updated name. |
| description | String (optional) | Updated description. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Updated project identifier. |
| success | Boolean | Whether the changes were saved. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12

### DELETE /api/v1/faculty/projects/{projectId}

Deletes the specified project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project to delete. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the project was deleted. |
| message | String | Deletion confirmation. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12

### POST /api/v1/faculty/projects/{projectId}/copy

Creates a copy of an existing project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Existing project being copied. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| newProjectId | Integer | Identifier of the copied project. |
| projectName | String | Name of the copied project. |
| success | Boolean | Whether the copy succeeded. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/copy

## Faculty — Skills

### GET /api/v1/faculty/projects/{projectId}/skills

Lists available projects.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the skills. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| skills | Array[Object] | Project skills, containing: |
| skillId | Integer | Skill identifier. |
| skillName | String | Name of the skill. |
| description | String | Description of the skill. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/skills

### POST /api/v1/faculty/projects/{projectId}/skills

Creates a new project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project receiving the skill. |
| skillName | String | Name of the new skill. |
| description | String | Explanation of the skill. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| skillId | Integer | Identifier of the new skill. |
| success | Boolean | Whether the skill was created. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/skills

### PATCH /api/v1/faculty/skills/{skillId}

Updates the specified skill.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| skillId | Integer | Skill being updated. |
| skillName | String (optional) | Updated skill name. |
| description | String (optional) | Updated description. |
| skillId | Integer | Updated skill identifier. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the changes were saved. |

**Example URL**

- api.example.com/api/v1/faculty/skills/5

### DELETE /api/v1/faculty/skills/{skillId}

Deletes the specified skill.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| skillId | Integer | Skill being deleted. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the skill was deleted. |
| message | String | Deletion confirmation. |

**Example URL**

- api.example.com/api/v1/faculty/skills/5

## Faculty — Scenarios

### GET /api/v1/faculty/projects/{projectId}/scenarios

Lists available projects.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the scenarios. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| scenarios | Array[Object] | Scenarios associated with the project. |
| scenarioId | Integer | Scenario identifier. |
| title | String | Scenario title. |
| body | String | Scenario description or storyline. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/scenarios

### POST /api/v1/faculty/projects/{projectId}/scenarios

Creates a new project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project receiving the scenario. |
| title | String | Scenario title. |
| body | String | Scenario storyline. |
| senderCharacterId | Integer | Character delivering the scenario. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| scenarioId | Integer | Identifier of the new scenario. |
| success | Boolean | Whether the scenario was created. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/scenarios

### GET /api/v1/faculty/scenarios/{scenarioId}

Retrieves the requested scenario information.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| scenarioId | Integer | Scenario being retrieved. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| scenarioId | Integer | Scenario identifier. |
| title | String | Scenario title. |
| body | String | Scenario storyline. |
| senderCharacterId | Integer | Assigned character. |
| options | Array[Object] | Available response options. |

**Example URL**

- api.example.com/api/v1/faculty/scenarios/7

### PATCH /api/v1/faculty/scenarios/{scenarioId}

Updates the specified scenario.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| scenarioId | Integer | Scenario being updated. |
| title | String (optional) | Updated title. |
| body | String (optional) | Updated storyline. |
| senderCharacterId | Integer (optional) | Updated character. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| scenarioId | Integer | Updated scenario identifier. |
| success | Boolean | Whether the changes were saved. |

**Example URL**

- api.example.com/api/v1/faculty/scenarios/7

### DELETE /api/v1/faculty/scenarios/{scenarioId}

Deletes the specified scenario.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| scenarioId | Integer | Scenario being deleted. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the scenario was deleted. |
| message | String | Deletion confirmation. |

**Example URL**

- api.example.com/api/v1/faculty/scenarios/7

### POST /api/v1/faculty/scenarios/{scenarioId}/options

Adds a selectable response option to a scenario.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| scenarioId | Integer | Scenario receiving the option. |
| responseText | String | Text of the selectable response. |
| skillId | Integer | Skill associated with this response for grading. |
| nextScenarioId | Integer or Null (optional) | Scenario shown if this response is selected. |
| optionId | Integer | Identifier of the new response option. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the option was created. |

**Example URL**

- api.example.com/api/v1/faculty/scenarios/7/options

### PATCH /api/v1/faculty/options/{optionId}

Updates an existing scenario response option.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| optionId | Integer | Response option being updated. |
| responseText | String (optional) | Updated response text. |
| nextScenarioId | Integer or Null (optional) | Updated branching destination |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| optionId | Integer | Updated option identifier. |
| success | Boolean | Whether the changes were saved. |

**Example URL**

- api.example.com/api/v1/faculty/options/21

### DELETE /api/v1/faculty/options/{optionId}

Deletes a scenario response option.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| optionId | Integer | Response option being deleted. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the option was deleted. |
| message | String | Deletion confirmation. |

**Example URL**

- api.example.com/api/v1/faculty/options/21

## Faculty — Characters (Personas)

### GET /api/v1/faculty/projects/{projectId}/characters

Lists available projects.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the characters. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| characters | Array[Object] | Characters associated with the project. |
| characterId | Integer | Character identifier. |
| characterName | String | Character's name. |
| jobTitle | String | Character's job title. |
| description | String | Character background. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/characters

### POST /api/v1/faculty/projects/{projectId}/characters

Creates a new project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project receiving the character. |
| characterName | String | Name of the character. |
| jobTitle | String | Character's job title. |
| description | String | Character background or role. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| characterId | Integer | Identifier of the new character. |
| success | Boolean | Whether the character was created. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/characters

### PATCH /api/v1/faculty/characters/{characterId}

Updates the specified character.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| characterId | Integer | Character being updated. |
| characterName | String (optional) | Updated name. |
| jobTitle | String (optional) | Updated title. |
| description | String (optional) | Updated description. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| characterId | Integer | Updated character identifier. |
| success | Boolean | Whether the changes were saved. |

**Example URL**

- api.example.com/api/v1/faculty/characters/4

### DELETE /api/v1/faculty/characters/{characterId}

Deletes the specified character.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| characterId | Integer | Character being deleted. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the character was deleted. |
| message | String | Deletion confirmation |

**Example URL**

- api.example.com/api/v1/faculty/characters/4

## Faculty — Resources

### GET /api/v1/faculty/projects/{projectId}/resources

Lists available projects.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the resources. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| resources | Array[Object] | Resources associated with the project. |
| resourceId | Integer | Resource identifier. |
| resourceName | String | Name of the resource. |
| description | String | Resource description. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/resources

### POST /api/v1/faculty/projects/{projectId}/resources

Creates a new project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project receiving the resource. |
| resourceName | String | Name of the resource. |
| description | String | Resource description. |
| file | File (binary) | Document being uploaded. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| resourceId | Integer | Identifier of the new resource. |
| success | Boolean | Whether the upload succeeded. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/resources

### PATCH /api/v1/faculty/resources/{resourceId}

Updates the specified resource.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| resourceId | Integer | Resource being updated. |
| resourceName | String (optional) | Updated name. |
| description | String (optional) | Updated description. |
| file | File (optional) | Replacement document. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| resourceId | Integer | Updated resource identifier. |
| success | Boolean | Whether the changes were saved |

**Example URL**

- api.example.com/api/v1/faculty/resources/9

### DELETE /api/v1/faculty/resources/{resourceId}

Deletes the specified resource.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| resourceId | Integer | Resource being deleted. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the resource was deleted. |
| message | String | Deletion confirmation. |

**Example URL**

- api.example.com/api/v1/faculty/resources/9

### PATCH /api/v1/faculty/resources/{resourceId}/visibility

Updates when a project resource is visible to students.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| resourceId | Integer | Resource being configured. |
| visibility | Enum (always, after_scenario) | Determines when students can view the resource. |
| scenarioId | Integer (optional) | Scenario that must be reached before the resource becomes available. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| resourceId | Integer | Updated resource identifier. |
| visibility | String | Saved visibility setting. |
| success | Boolean | Whether the update succeeded. |

**Example URL**

- api.example.com/api/v1/faculty/resources/9/visibility

## Faculty — Gadgets

### GET /api/v1/faculty/projects/{projectId}/gadgets

Lists available projects.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the gadgets. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| gadgets | Array[Object] | Gadgets associated with the project. |
| gadgetId | Integer | Gadget identifier. |
| gadgetName | String | Gadget name. |
| gadgetType | String | Type of gadget. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/gadgets

### POST /api/v1/faculty/projects/{projectId}/gadgets

Creates a new project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project receiving the gadget. |
| gadgetName | String | Name of the gadget. |
| gadgetType | Enum | Type of gadget being created. |
| configuration | Object | Gadget content and display settings. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| gadgetId | Integer | Identifier of the new gadget. |
| success | Boolean | Whether the gadget was created. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/gadgets

### PATCH /api/v1/faculty/gadgets/{gadgetId}

Updates the specified gadget.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| gadgetId | Integer | Gadget being updated. |
| gadgetName | String (optional) | Updated gadget name. |
| gadgetType | Enum (optional) | Updated gadget type. |
| configuration | Object (optional) | Updated gadget settings. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| gadgetId | Integer | Updated gadget identifier. |
| success | Boolean | Whether the changes were saved. |

**Example URL**

- api.example.com/api/v1/faculty/gadgets/3

### DELETE /api/v1/faculty/gadgets/{gadgetId}

Deletes the specified gadget.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| gadgetId | Integer | Gadget being deleted. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the gadget was deleted. |
| message | String | Deletion confirmation. |

**Example URL**

- api.example.com/api/v1/faculty/gadgets/3

## Faculty — Inbox Configuration

### GET /api/v1/faculty/projects/{projectId}/inbox

Lists messages configured for a faculty project inbox.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the configured inbox. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| messages | Array[Object] | Messages configured for the project. |
| messageId | Integer | Message identifier. |
| scenarioId | Integer | Scenario associated with the message. |
| messageType | Enum (email, instant_message) | Type of message. |
| sequenceNumber | Integer | Position in the inbox sequence. |
| releaseCondition | String | Condition controlling delivery. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/inbox

### POST /api/v1/faculty/projects/{projectId}/inbox/messages

Adds a scenario message to a project inbox.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project receiving the message. |
| scenarioId | Integer | Scenario being added to the inbox. |
| messageType | Enum (email, instant_message) | Type of message. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | Integer | Identifier of the new inbox message. |
| success | Boolean | Whether the message was added. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/inbox/messages

### PATCH /api/v1/faculty/inbox/messages/{messageId}

Updates the order or release condition of an inbox message.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | Integer | Inbox message being updated. |
| sequenceNumber | Integer (optional) | Updated delivery order. |
| releaseCondition | Enum (immediate, after_previous) | Condition controlling when the message becomes available. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | Integer | Updated message identifier. |
| success | Boolean | Whether the changes were saved. |

**Example URL**

- api.example.com/api/v1/faculty/inbox/messages/18

### DELETE /api/v1/faculty/inbox/messages/{messageId}

Removes a message from the project inbox.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | Integer | Inbox message being removed. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the message was removed. |
| message | String | Removal confirmation. |

**Example URL**

- api.example.com/api/v1/faculty/inbox/messages/18

### POST /api/v1/faculty/inbox/messages/{messageId}/resources

Attaches a resource to a faculty inbox message.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | Integer | Message receiving the attachment. |
| resourceId | Integer | Resource being attached. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| messageId | Integer | Message identifier. |
| resourceId | Integer | Attached resource identifier. |
| success | Boolean | Whether the attachment was added. |

**Example URL**

- api.example.com/api/v1/faculty/inbox/messages/18/resources

### GET /api/v1/faculty/projects/{projectId}/inbox/preview

Shows faculty a preview of the student inbox.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project whose inbox is being previewed. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| messages | Array[Object] | Preview of the configured student inbox. |
| messageId | Integer | Message identifier. |
| subject | String | Message title. |
| senderName | String | Sending character. |
| sequenceNumber | Integer | Message display order. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/inbox/preview

## Faculty — Administrative Settings

### POST /api/v1/faculty/projects/{projectId}/students

Assigns students to a faculty project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project receiving the students. |
| studentIds | Array[Integer]: I | Ds of students being assigned. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| assignedCount | Integer | Number of students successfully assigned. |
| success | Boolean | Whether the assignments succeeded. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/students

### DELETE /api/v1/faculty/projects/{projectId}/students/{studentId}

Removes a student from a faculty project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the student. |
| studentId | Integer | Student being removed. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| success | Boolean | Whether the student was removed. |
| message | String | Removal confirmation. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/students/45

### PATCH /api/v1/faculty/projects/{projectId}/availability

Sets the dates when students can access a project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project being configured. |
| startDate | Datetime | Date students can begin accessing the project. |
| endDate | Datetime | Date student access ends. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Updated project identifier. |
| success | Boolean | Whether availability settings were saved. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/availability

### PATCH /api/v1/faculty/projects/{projectId}/status

Changes the current status of a project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project being updated. |
| status | Enum (draft, active, completed) | Updated project status. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Updated project identifier. |
| status | String | Saved project status. |
| success | Boolean | Whether the status was updated. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/status

## Faculty — Results and Grading

### GET /api/v1/faculty/projects/{projectId}/results

Lists student performance results for a faculty project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing student results. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| results | Array[Object] | Student performance records. |
| studentId | Integer | Student identifier. |
| studentName | String | Student's name. |
| totalScore | Integer | Student's total score. |
| status | String | Assessment completion status. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/results

### GET /api/v1/faculty/projects/{projectId}/students/{studentId}/responses

Retrieves a student’s submitted responses for a project.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the responses. |
| studentId | Integer | Student whose answers are being viewed. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| responses | Array[Object] | Student's submitted answers. |
| responseId | Integer | Response identifier. |
| scenarioId | Integer | Scenario being answered. |
| selectedOptionId | Integer | Selected answer. |
| score | Integer | Points earned for the response. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/students/45/responses

### GET /api/v1/faculty/projects/{projectId}/students/{studentId}/skills

Retrieves a student’s scores for each evaluated skill.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the skill scores. |
| studentId | Integer | Student whose skills are being evaluated. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| skillScores | Array[Object] | Student's scores across evaluated skills. |
| skillId | Integer | Skill identifier. |
| skillName | String | Name of the evaluated skill. |
| score | Integer | Points earned for that skill. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/students/45/skills

### PATCH /api/v1/faculty/projects/{projectId}/students/{studentId}/responses/{responseId}

Updates a student response score and faculty feedback.

**Input:**

| Name | Type | Description |
| --- | --- | --- |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| responseId | Integer | Updated response identifier. |
| updatedScore | Integer | Saved score. |
| success | Boolean | Whether the grade was updated. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/students/45/responses/108

### GET /api/v1/faculty/projects/{projectId}/grades/export?format=pdf

Exports the project’s student grades as a downloadable report.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project whose grades are being exported. |
| format | Enum (pdf, xlsx) | Requested export format. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| file | Binary | Generated grade report in the requested format. |
| contentType | String (HTTP header) | File media type, such as application/pdf. |
| contentDisposition | String (HTTP header) | Suggested download filename. |

**Example URL**

- api.example.com/api/v1/faculty/projects/12/grades/export?format=pdf
