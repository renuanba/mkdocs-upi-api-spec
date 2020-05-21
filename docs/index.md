# **UPI API Specifications**

All APIs are exposed as stateless service over HTTPS. PSP should ensure idempodent behaviour for all APIs. Usage of open data format in XML and widely used protocol such as HTTP allows easy adoption by the members.  

API input data should be sent to the following URL as XML document using Content-Type “application/xml” or “text/xml”.  

```text
https://<host>/upi/<api>/<ver>/urn:txnid:<txnId>
```


> * ***host*** – API server address (Actual production server address will be provided to members at the time of rollout and all API clients should ensure that actual URL is configurable). 
> * ***upi*** – static value denoting the root of all API URL paths under the Unified Payments Interface. 
> * ***api*** – name of the API URL endpoint. 
> * ***ver*** – version of the API. Multiple versions of the same API may be available for supporting gradual migration. As of this specification, default version is "1.0|2.0". 
> * ***txnId*** – Transaction id which will be used for load balancing purpose at UPI end 

<br />


All APIs have same ack response as given below: 

```xml
<upi:Ack xmlns:upi="" api="" reqMsgId="" errCode="" ts=""/>
```

> * ***Ack*** – root element name of the acknowledgement message. 
> * ***api*** – name of the API for which acknowledgement is given out. 
> * ***reqMsgId*** - message ID of the input for which the acknowledgement is given out. 
> * ***err*** - this denotes any error in receiving the original request message. 
> * ***ts*** - timestamp of the acknowledgement sent by the receiver. 

<br />

