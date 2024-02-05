# Optimizing S3 Performance 
**Types of Prefixes :** 
1. mybucketname/folder1/subfolder1/myfile.jpg > /folderl/subfolder
2. mybucketname/folder2/subfolder1/myfile.jpg > /folder2/subfolder1
3. mybucketname/folder3/myfile.jpg >/folder3
4. mybucketname/folder4/subfolder4/myfile.jpg > /folder4/subfolder4
>S3 has extremely low latency. You can get the first byte out of S3 within 100-200 milliseconds.
You can also achieve a high number of requests: 3,500
PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second, per prefix.
- You can get better performance by spreading your reads across different prefixes. For example, if you are using 2
prefixes, you can achieve 11,000 requests per second.
- If we used all 4 prefixes in the last example, you would achieve 22,000 requests per second.
### S3 LIMITATIONS WHEN USING KMS
- If you are using SSE-KMS to encrypt your objects in S3, you must keep in mind the KMS limits.
- When you upload a file, you will call GenerateDataKey in the KMS API.
- When you download a file, you will call Decrypt in the KMS API.
### KMS Request Rates
- Uploading/downloading will count toward the KMS quota.
- Region-specific, however, it's either 5,500, 10,000, or 30,000 requests per second.
- Currently, you cannot request a quota increase for KMS.
## S3 Performance: Uploads
**Multipart Uploads**
- Recommended for files over 100 MB
- Required for files over 5 GB
- Parallelize uploads (increases efficiency)
![Alt text](/Photos/s3-performance.png)
## S3 Performance: Downloads
**S3 Byte-Range Fetches**
- Parallelize downloads by specifying byte ranges.
- If there's a failure in the download, it's only for a specific byte range.
![Alt text](/Photos/s3-performance-downloads.png)