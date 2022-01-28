# Amazon S3 - Default Encryption

Using default encryption, you are able to set a default encryption mechanism for every new object that is uploaded to the bucket. Do note that for any objects that are already in your bucket prior to enabling default encryption, they will **not** be encrypted.

There are two types of default encryptions:


## SSE-S3 (AES-256)

Server-Side Encryption with S3 Managed Keys, SSE-S3 Server-side encryption with S3 managed keys, SSE-S3 requires minimal configuration and all management of the encryption keys used are managed by AWS.

### encryption
- A client uploads Object Data to S3.
- S3 then takes this Object Data and encrypts it with an S3 Plaintext Data Key 
- This creates an encrypted version of the Object Data, which is then saved and stored on S3
- Next, the S3 Plaintext Data Key is encrypted with an S3 Master Key, which creates an encrypted S3 Data Key. 
- This encrypted Data Key is then also stored on S3 and the Plaintext Data Key is removed from memory.

### decryption
- A request is made by the client to S3 to retrieve the Object Data.
- S3 takes the associated encrypted S3 Data Key of the Object Data and decrypts it with the S3 Master Key.
- The S3 Plaintext Data Key is then used to decrypt the object data.
- This object data is then sent back to the client.

## SSE-KMS
SSE-KMS allows S3 to use the key management service (KMS) to generate your data encryption keys. 

Using KMS gives you far greater flexibility of how your keys are managed. For example, you are able to disable, rotate, and apply access controls to the CMK, and audit against their usage using AWS Cloud Trail.

### encryption
- A client uploads object data to S3.
- S3 then requests data keys from a KMS-CMK.
- Using the specified CMK, KMS generates two data keys, a plain text data key and an encrypted version of the same data key.
- These two keys are then sent back to S3. S3 then combines the object data and the plain text data key to perform the encryption.
- This creates an encrypted version of the object data which is then stored on S3 along with the encrypted data key.
- The plain text data key is then removed from memory.

### decryption
- A request is made by the client to S3 to retrieve the object data
- S3 sends the associated encrypted data key of the object data to KMS.
- KMS then uses the correct CMK with the encrypted data key to decrypt it and create a plain text data key.
- This plain text data key is then sent back to S3.
- The plain text data key is then combined with the encrypted object data to decrypt it.
- This decrypted object data is then sent back to the client.