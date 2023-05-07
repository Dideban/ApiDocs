# Errors

```json
#Error response body is always an array of objects with a key and a message. Here are a few examples:

[
    {
        "key": "Id",
        "message": "Id is required."
    }
]

[
    {
        "key": "not_found",
        "message": "وب‌سایت با شناسه مورد نظر یافت نشد."
    }
]
```
<aside class="notice">
This section provides a list of error codes you may encounter if a request is sent with incorrect formatting or if there is an issue with our servers.
</aside>

Dideban API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request – Your request is malformed or invalid.
401 | Unauthorized – Your token is either invalid or has expired.
403 | Forbidden – You lack the necessary permissions to access this resource.
404 | Not Found – The specified entity could not be located.
429 | Too Many Requests – You are sending requests at a rate exceeding our limits. Please slow down.
500 | Internal Server Error – An issue has occurred on our server. Please try again later.
503 | Service Unavailable – Our servers are temporarily offline for maintenance. Check back soon.
504 | Gateway Timeout – A serious issue has likely occurred, but don't worry, we're working on it.
