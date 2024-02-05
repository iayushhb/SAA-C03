# Encrypting S3 Objects -

## Types of Encryption : 
1. **Encryption in Transit** :
    
    When the traffic passing between one endpoint to another is indecipherable. Anyone eavesdropping between server A and server B won’t be able to make sense of the information passing by. Encryption in transit for S3 is always achieved by SSL/TLS.
    - SSL/TLS
    - HTTPS
2. **Encryption at Rest**: 

    When the immobile data sitting inside S3 is encrypted. If someone breaks into a server, they still won’t be able to access encrypted info within that server. Encryption at rest can be done either on the server-side or the client-side. The server-side is when S3 encrypts your data as it is being written to disk and decrypts it when you access it. The client-side is when you personally encrypt the object on your own and then upload it into S3 afterwards.

    ### Server-Side Encryption -
    *You encrypt files after uploading them to the cloud.*

    **S3 Managed Keys / SSE - S3 (server side encryption S3 )** 
    
    >When Amazon manages the encryption and decryption keys for you automatically. In this scenario, you concede a little control to Amazon in exchange for ease of use.

    **AWS Key Management Service / SSE - KMS**
    
    >When Amazon and you both manage the encryption and decryption keys together.

    **Server Side Encryption w/ customer provided keys / SSE - C**
    >When I give Amazon my own keys that I manage. In this scenario, you concede ease of use in exchange for more control.

    ### Client-Side Encryption -

    *You encrypt the files yourself before you upload them to S3.*

> All Amazon S3 Buckets have encryption configured by default.
All objects are automatically encrypted by using server-side encryption with Amazon S3 managed keys(SSE-S3).
Applies to all objects in your S3 bucket.

Every time a file is uploaded to S3, a PUT request is initiated.
![Alt text](/Photos/put-request.png)

## Enforcing Server-Side Encryption using bucket policy
1. **x-amz-server-side-encryption** 

    If the file is to be encrypted at the upload time, the `x-amz-server-side-encryption` parameter will be included in the request header.
2. You get 2 encryption types : 

    `x-amz-server-side-encryption : AES256`
    (SSE-S3- - S3-Managed keys)

    `x-amz-server-side-encryption : aws:kms`
    (SSE-KMS -- KMS-Managed keys)
3. **PUT Request Header**

    When this parameter is included in the header of the PUT request, it tell S3 to encrypt the object at the time of upload, using the specified encryption method.

![Alt text](/Photos/put-req.png)
> If you want to change the encryption type of any object then just go to the object in the bucket and scroll down and you'll see `Server-side encryption settings`.