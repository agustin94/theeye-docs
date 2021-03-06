# Script Task

[![theeye.io](../../images/logo-theeye-theOeye-logo2.png)](https://theeye.io/en/index.html)

## Popup Message

The Web Popup Message allows to display a friendly message to the users when a task completes the execution.

When a user executes a task using the Web Application and he awaits for the task result, that user alone will receive a one-time message in the Web Application using a separted popup message box.

The message can be any string defined within the script. At this moment there are two flovours to choose:

* A plain text message

* A simple list of items

The Popup Message will also interprete web links and will make them clickeable.


To emit a plain text message using the popup message box, the task result should be defined as follow

```json

  [{
    "popup_component": "Message with a clickable link: https://documentation.theeye.io" 
  }]

```

To display a list, the value for popup_component property should be changed to an array

```json

  [{
    "popup_component": [
      "Item 1",
      "Item 2",
      "info@theeye.io",
      "https://documentation.theeye.io"
    ] 
  }]

```


Let's try some code

```javascript

#!/usr/bin/node

try {
  const name = process.argv[2]
  const data = [{
    "popup_component": "Hi " + name + ", visit our documentation for more information! https://documentation.theeye.io"
  }]

  console.log( JSON.stringify( data ) )
} catch (e) {
  console.error(e)
  console.error('failure')
  process.exit(2)
}

```

You can download the recipe from this link.

[Popup Recipe](https://github.com/theeye-io/recipes/blob/master/task/script/Show_Popup_Message.json)


### Enable Popup

To enable this feature 

1. Open the task edition/creation form 

2. Go to the bottom and click **Advanced Options**

3. The **Result Popup** option must be checked



## Runtime Information

During runtime, you can access basic information of the job being executed via environment variables.

The information is storead as JSON Strings or as JSON encoded Key-Value structures.
All the environment variables belonging to TheEye runtime are prefixed with *THEEYE_* keyword

### THEEYE_JOB (object)

Contains information of the current job.

| Name | Type | Description |
| ---  | --- | --- |
| id | string | the id of the job. you can fetch the API with it |
| task_id | string | task definition id. can fetch the API with it |

### THEEYE_JOB_USER (object)

This is the user that executes the Task. This env will contain different values depending on how the task was executed.

* Automatic Execution: the user will be always a internal bot user.
* Play Button: When the task is executed via User Interface. This will be the user that pushed the Play Button.
* API Calls: Api calls can be done using Integration Keys (bot user) or Access Tokens (human user). The user would be a bot or a human.

| Name | Type | Description |
| ---  | --- | --- |
| id | string | the user id |
| email | string | the user email |

### THEEYE_JOB_WORKFLOW (object)

When Tasks belongs to Workflows, this constains information of the Workflow.

| Name | Type | Description |
| ---  | --- | --- |
| id | string | the workflow schema id |
| job_id | string | the workflow job execution instance |

### THEEYE_API_URL (string)

This is the default API URL.

### THEEYE_ORGANIZATION_NAME (string)

This is the organization name or project running the current script.

## Examples

###  Get user information from DOS / BAT scripts

The following script shows how to get user id and email information, it can be replicated to get information for THEEYE_JOB and THEEYE_JOB_WORKFLOW:
[Download Recipe](https://github.com/theeye-io/theeye-docs/blob/master/docs/assets/recipes/check_theeye_env_vars.json)

