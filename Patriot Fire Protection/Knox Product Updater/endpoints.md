# API Endpoint Reference
The **Knox Product Updater** provides a REST API for running updates and managing admin dashboard state. The following endpoints are used for the admin interface.

## Update
This is the primary endpoint for running a Knox product update. It utilizes the WordPress action scheduler to update product data from a CSV file in the background.

### Definition
`POST /wp-json/knox/v1/update`

### Arguments
| Parameter | Value                                      |
|-----------|--------------------------------------------|
| path      | (*string*) The direct path to the CSV file |

### Response
The successful response. This will be returned if the update has started without failure.
#### 200 Response
```json
{
  "status": "success",
  "message": "Update started."
}
```
The failed response. The will be returned if the update failed before finishing.
#### 500 Response
```json
{
  "status": "failed",
  "message": "CSV failed to parse. Please make sure the sheet you uploaded is formatted properly and try again."
}
```

## Check Status
This endpoint checks and sends back details regarding the current status of the update. It is useful in determining the state of the update admin page.

### Definition
`GET /wp-json/knox/v1/status`

### Arguments
No arguments available for this endpoint.

### Response
#### 200 Responses
The initial state, when the update has yet to be initiated.
```json
{
  "status": "not started",
  "message": "Awaiting update",
  "progress": -1
}
```
The state while the update is actively updating in the background. The "progress" property will range from 0-99 (percent).
```json
{
  "status": "in progress",
  "message": "An update is in progress",
  "progress": 50
}
```
The state once the update has completed.
```json
{
  "status": "complete",
  "message": "Update complete",
  "progress": 100
}
```
#### 500 Responses
The "message" property will vary based on error returned by the server.
```json
{
  "status": "failed",
  "message": "CSV failed to parse. Please make sure the sheet you uploaded is formatted properly and try again.",
  "progress": -1
}
```

## Update Status
This endpoint is designed to notify the database that the user has acknowledged a success or failed state so they can start over.

### Definition
`POST /wp-json/knox/v1/update-status`

### Arguments
No arguments available for this endpoint.

### Response
The successful response.
#### 200 Response
```json
{
  "status": "success",
  "message": "Status updated successfully"
}
```
The failed response. The "message" property will vary based on error returned by the server.
#### 500 Response
```json
{
  "status": "failed",
  "message": "Status failed to update."
}
```