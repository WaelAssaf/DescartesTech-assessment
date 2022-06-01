# DescartesTech-assessment

Implementation Tech Stack
•	C#
•	.NET Framework
•	JSON
•	Postman to run and manage the API requests

Usage Workflow
1.	Make sure the API is running.
2.	Encode the two binaries that you need to compare as Base64 string. You can use any online tool such as https://www.base64encode.org/
3.	Put these Base64 strings to JSON into data field.
4.	Pick an ID for the comparison.
5.	Send the binaries with PUT request to /api/v1/diff/:id/left and / api/v1/diff/:id/right URLs.
6.	Receive the comparison result with GET request to /api/v1/diff/:id URL.
7.	Use the JSON file names data.json to save the data uploaded and check the data.

API
Upload Binary
Upload binary as left or right object for comparison.
•	URL
/api/v1/diff/:id/left and /api/v1/diff/:id/right
•	Method:
PUT
•	Content
{"data": "<base64 encoded binary>"}
•	Success Response:
o	Code: 200
Binary was uploaded successfully to the JSON file
•	Error Response:
o	Exception
	The input is not base64 valid
OR
o	Code: 400 BAD REQUEST
Missing or invalid data parameter in the request body such as data is equal to null
•	Sample HTTP Request:
•	PUT /api/v1/diff/id/left
•	{"data":"AQIDBAUGBwgJAA=="}









Get Comparison Result
Get the comparison result of 2 previously uploaded binaries (left and right).
•	URL
/api/v1/diff/:id
•	Method:
GET
•	Success Response:
o	Code: 200
Comparison is successful

Content when binaries are exactly the same:
"diffResultType": "Equals

Content when binaries have different length:
"diffResultType": "SizeDoNotMatch"

Content when binaries have the same length but some differences exist (example):
	200 OK
	{
	"diffResultType": "ContentDoNotMatch",
	"diffs": [
	 {
	 "offset": 0,
	 "length": 1
	 },
	 {
	 "offset": 2,
	 "length": 2
	 }
	]
	}
•	Error Response:
o	Code: 404 NOT FOUND
One or both binaries with requested ID were not uploaded yet






