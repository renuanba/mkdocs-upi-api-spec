## List Accounts
PSPs to find the list of accounts linked to the mobile or Adhaar by a particular account
provider. If the destination bank name is not known details of account provider will be
fetched from central mapper.
As part of ATM PIN introduction, the issuer bank has to respond with new cred block with
subtype as ATM PIN, its type and length, where PIN length can be 4 or 6 digits. This info
will be used to capture ATM PIN in the common library.

### ReqListAccount

```xml
<upi:ReqListAccount xmlns:upi="http://npci.org/upi/schema/">
    <Head ver="1.0|2.0" ts="" orgId="" msgId="" />
    <Txn id="" note="" refId="" refUrl="" ts="" type="ListAccount" />
    <Link type="MOBILE|AADHAAR" value="" />
    <Payer addr="" name="" seqNum="" type="PERSON|ENTITY" code="" aadhaarConsent="Y|N">
        <Device>
            <Tag name="MOBILE" value=""/>
            <Tag name="GEOCODE" value=""/>
            <Tag name="LOCATION" value=""/>
            <Tag name="IP" value=""/>
            <Tag name="TYPE" value=""/>
            <Tag name="ID" value=""/>
            <Tag name="OS" value=""/>
            <Tag name="APP" value=""/>
            <Tag name="CAPABILITY" value=""/>
            <Tag name="TELECOM" value="Airtel|Vodafone"/>
        </Device>
        <Ac addrType="ACCOUNT">
            <Detail name="IFSC" value=""/>
        </Ac>
    </Payer>
</upi:ReqListAccount>
```

<br/>


### RespListAccount

```xml
<upi:RespListAccount xmlns:upi="http://npci.org/upi/schema/">
    <Head ver="1.0|2.0" ts="" orgId="" msgId=""/>
    <Txn id="" note="" refId="" refUrl="" ts="" type="ListAccount"/>
    <Resp reqMsgId="" result="SUCCESS|FAILURE" errCode=""/>
    <AccountList>
        <Account accType="SAVINGS|CURRENT|DEFAULT|NRE|NRO|CREDIT|PPIWALLET|BANKWALLET|SOD|UOD" 
                 mbeba="" accRefNumber="" maskedAccnumber="" ifsc="HDFC0000101" mmid="9056014" name="" aeba="Y|N"
                 aadhaarNo="1234 5678 9012">
            <CredsAllowed type="PIN" subType="ATMPIN" dType="" dLength=""/>
        </Account>
        <Account accType="SAVINGS|CURRENT|DEFAULT|NRE|NRO|CREDIT|PPIWALLET|BANKWALLET|SOD|UOD" mbeba="" 
                 accRefNumber="" maskedAccnumber="" ifsc="HDFC0000103" mmid="9056114" name="" aeba="Y|N">
            <CredsAllowed type="PIN" subType=" MPIN" dType="" dLength=""/>
            <CredsAllowed type="PIN" subType="ATMPIN" dType="" dLength=""/>
            <CredsAllowed type="OTP" subType="SMS" dType="" dLength=""/>
        </Account>
    </AccountList>
</upi:RespListAccount>
```

#### Comments
- mbeba flag is used to mention the UPI PIN availability
- If user consent for Aadhaar (aadhaarConsent) is "Y" and aeba="Y" then bank should send the Aadhaar no. Masked account.no should be masked with capital letter"X"

