# **List Accounts**
PSPs to find the list of accounts linked to the mobile or Adhaar by a particular account
provider. If the destination bank name is not known details of account provider will be
fetched from central mapper.
As part of ATM PIN introduction, the issuer bank has to respond with new cred block with
subtype as ATM PIN, its type and length, where PIN length can be 4 or 6 digits. This info
will be used to capture ATM PIN in the common library.

<br />

=== "ReqListAccount"
    ```xml  hl_lines="6 17"
    <upi:ReqListAccount xmlns:upi="http://npci.org/upi/schema/">                                                            
        <Head ver="1.0|2.0" ts="" orgId="" msgId="" />
        <Txn id="" note="" refId="" refUrl="" ts="" type="ListAccount" />
        <Link type="MOBILE|AADHAAR" value="" />
        <Payer addr="" name="" seqNum="" type="PERSON|ENTITY" code="" 
               aadhaarConsent="Y|N" >
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

=== "RespListAccount"
    ```xml hl_lines="6 11"
    <upi:RespListAccount xmlns:upi="http://npci.org/upi/schema/">
        <Head ver="1.0|2.0" ts="" orgId="" msgId=""/>
        <Txn id="" note="" refId="" refUrl="" ts="" type="ListAccount"/>
        <Resp reqMsgId="" result="SUCCESS|FAILURE" errCode=""/>
        <AccountList>
            <Account accType="SAVINGS|CURRENT|DEFAULT|NRE|NRO|CREDIT|PPIWALLET|BANKWALLET|SOD|UOD" 
                     mbeba="" accRefNumber="" maskedAccnumber="" ifsc="HDFC0000101" mmid="9056014" 
                     name="" aeba="Y|N" aadhaarNo="1234 5678 9012">
                <CredsAllowed type="PIN" subType="ATMPIN" dType="" dLength=""/>
            </Account>
            <Account accType="SAVINGS|CURRENT|DEFAULT|NRE|NRO|CREDIT|PPIWALLET|BANKWALLET|SOD|UOD" 
                     mbeba="" accRefNumber="" maskedAccnumber="" ifsc="HDFC0000103" mmid="9056114" 
                     name="" aeba="Y|N">
                <CredsAllowed type="PIN" subType=" MPIN" dType="" dLength=""/>
                <CredsAllowed type="PIN" subType="ATMPIN" dType="" dLength=""/>
                <CredsAllowed type="OTP" subType="SMS" dType="" dLength=""/>
            </Account>
        </AccountList>
    </upi:RespListAccount>
    ```

<details><summary style="font-size:14pt">Tag Description</summary>
    <table>
        <tr><th style="background-color:DodgerBlue">Tag Num</th><th style="background-color:DodgerBlue">Message Item</th><th style="background-color:DodgerBlue">XML Tag</th><th style="background-color:DodgerBlue">Occurrence</th></tr>
        <tr><td>24.1</td><td>Linked account list</td><td>&lt;Link&gt;</td><td>1..1</td></tr>
        <tr><td>24.1.2</td><td>Account linkage to Mobile/Aadhaar </td><td>type</td><td>1..1</td></tr>
        <tr><td>24.1.3</td><td>Mobile or Aadhaar Number</td><td>value</td><td>1..1</td></tr>
        <tr><td><mark>24.1.4</mark></td><td><mark>Aadhaar Consent</mark></td><td><mark>aadhaarConsent</mark></td><td><mark>1..1</mark></td></tr>
        <tr><td><mark>24.1.5</mark></td><td><mark>TELECOM Operator</mark></td><td><mark>value</mark></td><td><mark>1..n</mark></td></tr>
    </table>
</details>

<details><summary style="font-size:14pt">Error and Response Codes</summary>
<table cellpadding=".5px">
    <tr><th style="background-color:DodgerBlue">Error Code</th><th style="background-color:DodgerBlue">Message Details</th><th style="background-color:DodgerBlue">Element/Tag</th><th style="background-color:DodgerBlue">Attribute</th></tr>
    <tr><td>U17</td><td>PSP IS NOT REGISTERED</td><td>&lt;Head/&gt;</td><td>orgId </td></tr>
    <tr><td>U52</td><td>PSP ORGID NOT FOUND</td><td>&lt;Head/&gt;</td><td>orgId </td></tr>
    <tr><td>Z02</td><td>VER NUMERIC/DECIMAL MIN LENGTH 1 MAX LENGTH 6</td><td>&lt;Head/&gt;</td><td>ver </td></tr>
    <tr><td>Z03</td><td>TS MUST BE ISO_ZONE FORMAT</td><td>&lt;Head/&gt;</td><td>ts </td></tr>
    <tr><td>Z06</td><td>MSGID MUST BE PRESENT MAXLENGTH 35</td><td>&lt;Head/&gt;</td><td>msgId </td></tr>
    <tr><td>P01</td><td>PAYER NOT PRESENT</td><td>&lt;Payer/&gt;</td><td></td></tr>
    <tr><td>P02</td><td>PAYER.ADDR MUST BE VALID VPA MAXLENGTH 255</td><td></td><td>addr</td></tr>
    <tr><td>P03</td><td>PAYER.NAME ALPHANUMERIC MINLEGTH 1 MAXLENGTH 99</td><td></td><td>name</td></tr>
    <tr><td>P04</td><td>PAYER.SEQNUM NUMERIC MINLEGTH 1 MAXLENGTH 3</td><td></td><td>seqNum</td></tr>
    <tr><td>P05</td><td>PAYER.TYPE MUST BE PRESENT/VALID</td><td></td><td>type</td></tr>
    <tr><td>P06</td><td>PAYER.CODE NUMERIC OF LENGTH 4</td><td></td><td>code</td></tr>
    <tr><td><mark>P09</mark></td><td><mark>PAYER.AADHAARCONSENT MUST BE PRESENT</mark></td><td></td><td><mark>aadhaarConsent</mark></td></tr>
    <tr><td>Y01</td><td>LINK NOT PRESENT</td><td>&lt;Link/&gt;</td><td></td></tr>
    <tr><td>Y02</td><td>LINK.TYPE MUST BE PRESENT/VALID</td><td></td><td>type</td></tr>
    <tr><td>Y03</td><td>LINK.VALUE MUST BE PRESENT/VALID</td><td></td><td>value</td></tr>
</table>
</details>

!!! important
    - mbeba flag is used to mention the UPI PIN availability
    - If user consent for Aadhaar (aadhaarConsent) is "Y" and aeba="Y" then bank should send the Aadhaar no. 
    - Masked account.no should be masked with capital letter "X"

