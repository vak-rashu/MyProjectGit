![aws infrastructure](https://github.com/user-attachments/assets/b9fc9d76-3abc-4a1e-b269-a8a75e05acb7)

## What is happening in the diagram?
1. The API Gateway has two endpoints created one for POST and another to GET, and they both are integrated to one lambda function which handles both the request.

![a user made a request to POST](https://github.com/user-attachments/assets/bd78aa2c-ee5e-4c80-87d6-455c2ba7576a)

- When a user wants to convert a file into link, he/she will go to POST /shorten and the lambda will put that object into the S3, with the key name being the filename given by the user.
Then a shortKey and Pre Signed URL of that object will be created, with a TimeToLive attribute of 5 mins only. So the user gets total 5 mins of time to use the URL to share or copy paste it into the browser to download the file. All this data will be stored in DynamoDB to create a mapping between the three keys.
- In return to the POST request he gets the generated shortened URL.

![the file being downloaded after the GET request](https://github.com/user-attachments/assets/8d379887-00af-4db4-b744-152a9a8dbc56)
- Now with this URL, the user would like to copy it and share it or paste it in some other browser to GET the download of the file.
This is done by actually redirecting the location to the corresponding Pre Signed URL, and the download will start automatically.
