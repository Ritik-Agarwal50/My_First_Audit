### [S-#] Stroing the password on chain makes it visible to anyone and no longer [private]


**Description:** 
All data stored on-chain is visible to anyonw and can be read directly from the blockchain. 
The `PasswordStore::s_password` vairable is intended to be private variable and only aces by the owner thorugh `PasswordStore::getPassword` function which is intended to be called by the owner only.


**Impact:** Anyooone can read the private password serverly breaking the funcationality of the protocol.  

**Proof of Concept:**(Proof of Code) 

Below test case show that anyone can access the password from on-chain.

1. Spin up the anvil blockchain
    ```
    make anvil
    ```
2. Deploy the contract
    ```
     make deploy
     ```
3. Run the storage tool: 
    ```
        cast storage <adress_here> 1 --rpc-url http://127.0.0.1:8545
    ```
     we use `1` beacuse at that storage `s_password` is storage.

     You then parse the hex to a string with:
     ```
        cast parse-bytes32-string 0x6d7950617373776f726400000000000000000000000000000000000000000014
    ```
    And get an output of:
    ```
    mypassword
    ```

**Recommended Mitigation:**  Because of above reason the entire protocol gets failed. One can br done is encryp the passwor off-chain nd store on blockchain but the user need to another password to decrypt the encrypt password.