# SETUP
Install the fabric-client and fabric-ca-client node modules
```sh
npm install
```
Launch the app
```sh
PORT=4000 node app
```
In a separate terminal run the REST API request examples.

# REST API REQUEST EXAMPLES
```
curl -s -X POST http://localhost:4000/users -H "content-type: application/x-www-form-urlencoded" -d 'username=Jim&orgName=Org1'
```

Save the token returned to environmental variable BEARERTOKEN

```
curl -s -X POST \
  http://localhost:4000/channels \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json" \
  -d '{
    "channelName":"mychannel",
    "channelConfigPath":"../artifacts/channel.tx"
}'
```

```
curl -s -X POST \
  http://localhost:4000/channels/mychannel/peers \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json" \
  -d '{
	  "peers": ["peer0.org1.hyperfabric.xyz"]
}'
```

```
curl -s -X POST \
  http://localhost:4000/chaincodes \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json" \
  -d '{
	"peers": ["peer0.org1.hyperfabric.xyz"],
	"chaincodeName":"mycc",
	"chaincodePath":"mychaincode",
	"chaincodeType": "golang",
	"chaincodeVersion":"v0"
}'
```

```
curl -s -X POST \
  http://localhost:4000/channels/mychannel/chaincodes \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json" \
  -d '{
	"peers": ["peer0.org1.hyperfabric.xyz"],
	"chaincodeName":"mycc",
	"chaincodeVersion":"v0",
	"chaincodeType": "golang",
	"args":[]
}'
```

```
curl -s -X POST \
  http://localhost:4000/channels/mychannel/chaincodes/mycc \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json" \
  -d '{
	"peers": ["peer0.org1.hyperfabric.xyz"],
	"fcn":"createCourse",
	"args":["AAAA","CourseA"]
}'
```

```
curl -s -X GET \
  "http://localhost:4000/channels/mychannel/chaincodes/mycc?peer=peer0.org1.hyperfabric.xyz&fcn=query&args=%5B%22AAAA%22%5D" \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json"
```

```
curl -s -X GET \
  "http://localhost:4000/channels/mychannel/blocks/1?peer=peer0.org1.hyperfabric.xyz" \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json"
```

```
curl -s -X GET http://localhost:4000/channels/mychannel/transactions/$TRANSACTIONID?peer=peer0.org1.hyperfabric.xyz \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json"
```

```
curl -s -X GET \
  "http://localhost:4000/channels/mychannel?peer=peer0.org1.hyperfabric.xyz" \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json"
```

```
curl -s -X GET \
  "http://localhost:4000/chaincodes?peer=peer0.org1.hyperfabric.xyz&type=installed" \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json"
```

```
curl -s -X GET \
  "http://localhost:4000/chaincodes?peer=peer0.org1.hyperfabric.xyz&type=instantiated" \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json"
```

```
curl -s -X GET \
  "http://localhost:4000/channels?peer=peer0.org1.hyperfabric.xyz" \
  -H "authorization: Bearer $BEARERTOKEN" \
  -H "content-type: application/json"
```
