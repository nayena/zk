# Amazon S3 - Requester Pays

As the name implies, when this feature is configured any costs associated with requests and data transfer becomes the responsibility of the requester instead of the bucket owner. 

The bucket owner will still, however, pay for the storage costs associated with the objects stored in the bucket.

A fundamental condition of enabling requester pays is ensuring that **all access is authenticated** to your bucket, as anonymous access requests will not be able to take advantage of the requester pays attribute.

From this point, any POST, GET or HEAD requests to the bucket must include x-amz-request-payer in the header and this parameter confirms that the requester is aware that there are cost implications associated with that request for requester pays.

These are the conditions where the bucket owner *still* is charged:
-   The requester doesn't include the parameter x-amz-request-payer in the header (GET, HEAD, or POST) or as a parameter (REST) in the request (HTTP code 403).
-   Request authentication fails (HTTP code 403).
-   The request is anonymous (HTTP code 403).
-   The request is a SOAP request.