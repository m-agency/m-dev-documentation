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
#### 200 Response
```json
{
  status: "success";
  message: "Update started.";
}
```
#### 500 Response
```json
{
  status: "failed";
  message: "CSV failed to parse. Please make sure the sheet you uploaded is formatted properly and try again.";
}
```

## Check Status
This endpoint checks and sends back details regarding the current status of the update. It is useful in determining the state of the update admin page.

### Definition
`GET /wp-json/knox/v1/status`

### Arguments
| Parameter | Value                                      |
|-----------|--------------------------------------------|
| path      | (*string*) The direct path to the CSV file |

### Response
#### 200 Response
```json
{
  status: "success";
  message: "Update started.";
}
```
#### 500 Response
```json
{
  status: "failed";
  message: "CSV failed to parse. Please make sure the sheet you uploaded is formatted properly and try again.";
}
```