# Errors

<!-- <aside class="notice">
This error section is stored in a separate file in <code>includes/_errors.md</code>. Slate allows you to optionally separate out your docs into many files...just save them to the <code>includes</code> folder and add them to the top of your <code>index.md</code>'s frontmatter. Files are included in the order listed.
</aside> -->

The Heysasha API uses the following error codes:

Error Code | Meaning | Description
---------- | ------- | ------- 
200 | OK | The request has succeeded. The meaning of a success varies depending on the HTTP method: GET: The resource has been fetched and is transmitted in the message body. PATCH: The resource has been updated.
201 | Created	| The request has succeeded and a new resource has been created as a result of it. This is typically the response sent after a POST request.
202	| Accepted | The request has succeeded and has been added to the queue, but the resource has not yet been created. This is typically the response sent after PUT and POST requests.
204	| No Content | There is no content to send for this request. This is common for DELETE requests.
400 | Bad Request | Your request is invalid.
401 | Unauthorized | Your API key is wrong.
403 | Forbidden | The kitten requested is hidden for administrators only.
404 | Not Found | The specified kitten could not be found.
405 | Method Not Allowed | You tried to access a kitten with an invalid method.
406 | Not Acceptable | You requested a format that isn't json.
409	| Conflict | Your request conflicts with the current state of the server.
410 | Gone | The kitten requested has been removed from our servers.
429 | Too Many Requests | You're requesting too many kittens! Slow down!
500 | Internal Server Error | We had a problem with our server. Try again later.
503 | Service Unavailable | We're temporarily offline for maintenance. Please try again later.
