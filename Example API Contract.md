##API Contract

### GET - `api/v1/some_endpoint`
Information about the API call. What is the intended behavior? When would this API call be used? 
#### Request
	{
		"payload":
		[
			{
				"identity": <uuid>,
				"key": <some value>
			}, ...
		]
	}
	
#### Response

HTTP Status Code 200 OK

-

### POST - `api/v1/another_endpoint`
Information about the API call. What is the intended behavior? When would this API call be used? 
#### Request
	{
		"payload":
		[
			{
				"identity": <uuid>,
				"key": <some value>
			}, ...
		]
	}
	
#### Response

HTTP Status Code 201 CREATED



