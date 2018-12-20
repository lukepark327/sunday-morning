# How to Use

## Install

### Environments

upper version 3.6, under version 3.7   
python 3.6.7 recommended

- tbears 1.0.6.2   
- requests 2.19.1

### OS

Only for macOS and Linux.

### Install LINE SDK

```bash
brew install leveldb
brew install rabbitmq
brew services start rabbitmq
```
```bash
mkdir work
cd work
```
```bash
virtualenv -p python3 .
source bin/activate
```
```bash
pip install tbears
```

## Start
```bash
$ cd work
$ source bin/activate
(work) $ tbears start
```

## Get Private Key
```bash
(work) $ tbears keystore <private.key>
```

## Deploy
```bash
(work) $ tbears deploy -k <keystore_file> [-c deploy_json] <contract_dir>
```
Get "scoreAddress" by ```tbears txresult <the above TxID>```.
- For example: ```cxc083078edbe951560728105235c235d6f5906c65```

## Call
```bash
(work) $ tbears call <call_json>
```

Or you can use **HTTP POST** instead:
```bash
curl -X POST http://127.0.0.1:9000/api/v3 -H"Content-Type: application/json; application/json" -d @<call_json>
```

Here is a sample of ```<call_json>``` below. Change "id", "from", "to", "method", and "params".

```javascript
{
    "jsonrpc": "2.0",
    "method": "icx_call",
    "id": 1234,
    "params": {
        "from"	: "hx27d99b5a1d8ffdd58bce204c303153a1a388eead",
        "to"	: "cx509430b08e156d002ade0e1cbdf0b2c5a5daad45",
        "dataType": "call",
        "data": {
            "method": "purchase",
            "params": {
                "_hash"	    : "0x0000123412341234123412341234123412341234123412341234123412341234",
				"_value"	: "100"
			}
        }
    }
}
```

## Stop
```bash
(work) $ tbears stop
```

## Delete deployed Contracts
```bash
$ tbears clear
```

<!--
////////////////////////////////////////
-->

# Demonstration

## Deploy LINK SCORE
[![video](http://img.youtube.com/vi/LRXtsxQeFec/0.jpg)](https://www.youtube.com/watch?v=LRXtsxQeFec)   
> Click on the image above to play the video.

## Call LINK SCORE's Functions
[![video](http://img.youtube.com/vi/aHySd_zohN8/0.jpg)](https://www.youtube.com/watch?v=aHySd_zohN8)   
> Click on the image above to play the video.

<!--
////////////////////////////////////////
-->

# Trouble Shooting

## pkg-config is required

```bash
'pkg-config' is required to install this package. Please see the README for details.
``` 

Do ```brew install pkg-config```, ```brew link pkg-config``` and ```pip install tbears```.

## tbears samples

```tbears samples``` causes an error like:
```bash
The samples command has been deprecated since v1.1.0 ...
```

When you receive the above error, go https://github.com/icon-project/samples, download files, move them into /work. Then do ```tbears deploy -k private.key hello_world/hello_world/```, Input your keystore password, step by step.

## Out of step

```javascript
    ...
    "failure": {
        "code": "0x7d64",
        "message": "Out of step: contractSet"
    }
    ...
```

When you receive an "Out of step" error, assign more "stepLimit" in the request message.

## put is not allowed

```javascript
    ...
    "jsonrpc": "2.0",
    "error": {
        "code": -32000,
        "message": "put is not allowed"
    }
    ...
```

When you receive an "put is not allowed" error, try this *stopgap*:
- Go to ```~/word/lib/python3.6/site-packages/iconservice/database/db.py```, ```_is_db_writable_on_context()```.
- Change the following code

    ```python
    	...
        return context_type != IconScoreContextType.QUERY and \
            func_type != IconScoreFuncType.READONLY
    ```

    to

    ```python
    	...
        return True
    ```

<!--
////////////////////////////////////////
-->
