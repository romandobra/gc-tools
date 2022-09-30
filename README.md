# gc-tools
Google Cloud bash scripts without gsutil

## Usage:
### gc-token
`gc-token KEY_FILE SCOPE [TOKEN_FILE [TOKEN_MAX_AGE]]`

Will generate `Authorization: Bearer` token for Google Cloud from the `.json` key file.
* KEY_FILE - location of your keyfile (example: `my-account_my-project.json`);
* SCOPE - access scope;
* TOKEN_FILE - (optional) location of your token if you have one and/or if you want to save the new one;
* TOKEN_MAX_AGE - (optional, default is 3600) access token time to live in seconds.

If you have a saved TOKEN_FILE, will check if it's not older than TOKEN_MAX_AGE. If it is older, the new token will be generated and TOKEN_FILE replaced.

Use the full SCOPE url from Google. Like `https://www.googleapis.com/auth/devstorage.read_write`

### gc-upload
`gc-upload TOKEN OBJECT_LOCATION BUCKET_NAME [OBJECT_NAME [OBJECT_CONTENT_TYPE]]`

Will upload the file to the Google Storage bucket.
* TOKEN - you can obtain one with `gc-token`;
* OBJECT_LOCATION - local file path you want to upload;
* BUCKET_NAME - your bucket name to upload to;
* OBJECT_NAME - (optional) remote path. Your file will be stored as `BUCKET/remote/path`. Default is the full local path without the trailing slash.
* OBJECT_CONTENT_TYPE - (optional, default is `application/octet-stream`) the media type you want the file to be served with.

## Combining both scripts
One line to get the token and upload a file:
`gc-upload $(gc-token KEY_FILE https://www.googleapis.com/auth/devstorage.read_write) OBJECT_LOCATION BUCKET_NAME`
