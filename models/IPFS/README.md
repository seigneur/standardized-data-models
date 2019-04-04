# Data Model Definitions

## List of Models

1. encryptedProfile
2. IPFSProfile
3. profileMetadataModel
4. requestForUploadingProfile

## Usage

This readme focuses on how we use the different data models come together and get integrated and encrypted and stored in IPFS. 

1. User Dapp calls t3-verifier node with the object requestForUploadingProfile.
2. Into IPFS the we write IPFSProfile.json and encryptedProfile.json
3. The profileMetadataModel is just the format of the various keys and values and alongwith the group definitions.
 
## Encryption Model

### Steps in Encryption

The encryption we can split into different types:

1. Client Side Encryption
2. Transport Encryption
3. Server Side Encryption
4. IPFS Encryption


#### Client side
On the client side for the data at rest in localstorage what we intend to do is:

1. The whole storage is then encrypted with PIN from user.
1. When we export, we export the encrypted profile.
1. When we import we ask User for pincode.
1.  Keep the pincode simple like 4/6 digit

#### Transport Encryption

We use https for transport to the t3v node and ipfs. 

#### Server Side Encryption 

Currently, we store the keys unencrypted, we will move this to encrypted storage in the server side Database. 

#### IPFS Side Encryption

1. We fetch random data as seed from random org, depending on how many groups that we may have.
2. We combine this with a PIN that the user gives us for now and create ppX-Z
3. Next we AES encrypt this data and send to IPFS
4. The keys are then send via requestForUploadingProfile to the T3 Verifier node who further dessiminates it, in future keys will be processed directly to the other verifiers.

However, in localstorage we do not store the combined ppX-Z but instead only the initial passphrase created from random org.

Thus if even storage is leaked, it only reveals part of the seed and not the user’s PIN.



## Version Information

TBD