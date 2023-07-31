# gcputils.test.connection_test

## Overview

The `connection_test` function tests the connection to Google Cloud Storage using Application Default Credentials. This function checks if the authentication to Google Cloud Storage works by using Application Default Credentials. These credentials are typically set up by running the 'gcloud auth application-default login' command.

If the connection is successful, it will list the buckets associated with the authenticated project.

## Note

Before running this function, ensure you have authenticated your application with Google Cloud using 'gcloud auth application-default login' or by setting up the necessary environment variables. 

## Raises

- `google.auth.exceptions.DefaultCredentialsError`: If the function fails to authenticate using Application Default Credentials.

## Example

```python
# Call the connection_test function to test the connection to Google Cloud Storage.
gcputils.test.connection_test()
```