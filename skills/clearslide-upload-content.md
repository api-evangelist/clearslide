---
name: Upload content to ClearSlide
description: Get S3 upload credentials, upload a file, and confirm the upload status.
api: openapi/clearslide-openapi.yml
operations: [postUpload, getUploadStatus]
---

# Upload content to ClearSlide

ClearSlide uses a two-step, S3-backed upload flow.

## Auth
- OAuth 2.0 bearer token (scope `write` to request credentials, `read` to check status). See
  `authentication/clearslide-authentication.yml`.

## Steps
1. **Request credentials** — `POST /upload` (`postUpload`) returns temporary credentials to upload
   your file directly to Amazon S3.
2. **Upload the file** — PUT the file to Amazon S3 using the returned credentials (see
   `developer.clearslide.com/docs/upload-file-to-amazon-s3`).
3. **Confirm status** — `GET /upload/{uploadID}` (`getUploadStatus`) to check that the uploaded
   file was processed.

## Notes
- Base URL: `https://platform.clearslide.com`. The S3 upload target is provided by step 1.
