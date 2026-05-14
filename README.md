# Error Documentation  TaskFlow API
The TaskFlow API returns standardized responses to indicate authentication failures, data validation issues, missing resources, and other error situations.
All errors follow the format:
{
"error": "Type of error",

"message": "Detailed description of the problem"
}

## Authentication

YoAll requests require a valid Bearer token in the header:
Authorization: Bearer tf-live-4a8f2c1e9b3d7e6a

---

## Error Codes 400   Bad Request
The server could not process the request due to invalid or missing data.
Possible causes: Missing required field
Invalid value
Invalid status
Malformed JSON

```
 Example  Missing required field
"error": "Bad Request",
  "message": "The 'name' field is required and must be a non-empty string."
  
 Example — Invalid status
  "error": "Bad Request",
  "message": "Invalid status 'completed'. Allowed values are: pending, in_progress, done."

 How to resolve
Check the required fields. Confirm the data types submitted. Use only the allowed values:
pending
in_progress
done
```
## 401  Unauthorized
This occurs when the API key is missing or invalid.

Example
{
  "error": "Unauthorized",
  "message": "Missing or invalid API key. Provide a valid key in the Authorization header as: Bearer <api_key>"
How to solve this:

Add the header correctly:
Authorization: Bearer tf-live-4a8f2c1e9b3d7e6a
```
 404   Not Found
The requested resource was not found.

This can happen when:

Updating a non-existent task
Deleting a non-existent task
Searching for tasks in a non-existent project
Creating tasks in projects that do not exist
Example — Project not found
{
  "error": "Not Found",
  "message": "No project found with project_id 'abc123'."
}
Example — Task not found
{
  "error": "Not Found",
  "message": "No task found with task_id 'abc123'."
```
## Correct workflow to avoid errors
The API has dependencies between resources. The recommended workflow is:
1. Create project
2. Create task within the project
3. Update task
4. List tasks
5. Delete task
If you try to create tasks without a valid project_id, the API will return a 404 Not Found error.
Best practices
Always validate IDs
```
## Before updating or deleting tasks:
confirm that the task_id exists
confirm that the project_id belongs to the correct project
```
## Use valid statuses
Only these values are accepted:
Status 				Description
pending 			Task not yet started
in_progress 	Task in progress
done 			  	Task completed
```
 Summary of errors
Code		 Name			 	Reason
400 		Bad Request			 Invalid or missing data
401 		Unauthorized 			API Key missing or invalid
404		 Not Found 			Project or task not found


