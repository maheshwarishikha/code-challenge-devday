# Code Challenge @IBM Developer Day

## Challenge

Interest Rate while creating a new asset should be increased by 2 when creates a entry in blockchain. Interface should also show the same.

For example, while creating a new asset if you provide interest rate as 10 then it should save as 12.

### Chaincode

`~/securitization_blockchain/chaincode/src` has `lib.go`, `securitization.go`, `read_ledger.go` and `write_ledger.go`.

### Find out
* which file you need to modify
* which function
* what code changes are required

### To compile chaincode locally

```
echo $GOROOT
/usr/local/go

echo $GOPATH

# Set GOPATH
export GOPATH=/home/student/fabric1.2

# Navigate to chincode directory ~/securitization_blockchain/chaincode/src
go build        ## It will be helpful to check for any errors in chaincode
OR 
go build -o <output binary name>

```

### Install Chaincode on your channel

`IBP Dashboard -> Channels -> Choose your channel -> Switch to Chaincode -> Install Chaincode -> Choose Peer -> Install Chaincode`

![](images/1.png)

* Provide same Chaincode ID as before.
* Chaincode Version should be different say v2.
* Choose all chaincode files.
* Click on `Submit`.

### Update your chaincode

Choose `Update` action for your installed chaincode as shown.

![](images/2.png)

### Configure Application

* Clean up the previous connection related details.
   ```
   cd ~/securitization_blockchain/sc-ui
   rm -f chaincode_info.json
   rm -f connection_profile.json
   rm -rf hfc-key-store
   ```
   
* Re-launch your application.
* Configure HF Client - with new version of chaincode.
* The previous entries will be shown on Application as-is.
* Now create a new asset and verify your updated chaincode.

### Code changes to be made

**Original Code** 
```
	asset.InterestRate = args[2]
```

**Updated Code**

```
	interest_rate, _ := strconv.ParseFloat(args[2], 32)
	interest_rate = interest_rate + 0.02
	asset.InterestRate = strconv.FormatFloat(interest_rate, 'f', -1, 32)
```




