
- [Overview](#overview)
- [APIs](#apis)
  - [KeyGen](#keygen)
  - [Encrypt](#encrypt)
  - [ReEncrypt](#reencrypt)
  - [Decrypt](#decrypt)


## Overview


**APIs corresponding to roles:**

- PADO Node, Compute node
  - [step1 KeyGen](#keygen)
  - [step4 ReEncrypt](#reencrypt)
- Data Provider, Seller
  - [step2 Encrypt](#encrypt)
- Data Consumer, Buyer
  - [step3. KeyGen](#keygen)
  - [step5. Decrypt](#decrypt)

<br/>

**Notes:**

- All **Input** and **Output** are json.


## APIs


### KeyGen

- for `Data Consumer` and `PADO Node`

**Input**

```
{
  "t": 2,         // type:number| 
  "n": 3,         // type:number| n >= 3; n >= t >= 1
  "indices": [],  // type:number-array| pado node index, start from 1
}
```

**Output**

```
{
  "sk": "", // type:string| secret key
  "pk": ""  // type:string| public key
}
```

### Encrypt

- only for `Data Provider`

 
**Input**

```
{
  "t": 2,             // type:number| 
  "n": 3,             // type:number| n >= 3; n >= t >= 1
  "indices": [],      // type:number-array| pado node index, start from 1
  "node_pks": [],     // type:string-array| pado node public keys, which length is equal to n
  "msg": [],          // type:byte-array| plain message (deprecated)
  "msg_ptr": number,  // type:number| the pointer to plain message
  "msg_len": number,  // type:number| the message size
}
```

**Output**

```
{
  "enc_sks": [],        // type:string-array| encrypted secret keys, which length is equal to n
  "nonce": "",          // type:string| nonce
  "enc_msg": "",        // type:string| encrypted message (deprecated)
  "emsg_ptr": number,   // type:number| the pointer to encrypted message
  "emsg_len": number,   // type:number| the message size
}
```



### ReEncrypt

- only for `PADO Node`


**Input**

```
{
  "t": 2,           // type:number| 
  "n": 3,           // type:number| n >= 3; n >= t >= 1
  "indices": [],    // type:number-array| pado node index, start from 1
  "enc_sk": "",     // type:string| data provider encrypted secrect key
  "node_sk": "",    // type:string| pado node secrect key
  "consumer_pk": "" // type:string| consumer publick key
}
```



**Output**

```
{
  "reenc_sk": "" // type:string| re-encrypted secrect key
}
```



### Decrypt

- only for `Data Consumer`


**Input**

```
{
  "t": 2,               // type:number| 
  "n": 3,               // type:number| n >= 3; n >= t >= 1
  "indices": [],        // type:number-array| pado node index, start from 1
  "chosen_indices": [], // type:number-array| selected nodes for computing
  "reenc_sks": [],      // type:string-array| re-encrypted secrect keys
  "consumer_sk": "",    // type:string| consumer secrect key
  "nonce": "",          // type:string| nonce
  "enc_msg": "",        // type:string| encrypted message (deprecated)
  "emsg_ptr": number,   // type:number| the pointer to encrypted message
  "emsg_len": number,   // type:number| the message size
}
```



**Output**

```
{
  "msg": [],          // type:byte-array| decrypted message (deprecated)
  "msg_ptr": number,  // type:number| the pointer to plain message
  "msg_len": number,  // type:number| the message size
}
```

