# Start
```bash
$ cd work
$ source bin/activate
(work) $ tbears start
```

# Deploy
```bash
(work) $ tbears deploy -k <keystore_file> [-c deploy_json] <contract_dir>
```
Get "scoreAddress" by ```tbears txresult <the above TxID>```.
- For example: ```cxc083078edbe951560728105235c235d6f5906c65```

# Call
```bash
(work) $ tbears call <call_json>
```

* ## Use HTTP POST
    ```bash
    curl -X POST http://127.0.0.1:9000/api/v3 -H"Content-Type: application/json; application/json" -d @<call_json>
    ```

# Stop
```bash
(work) $ tbears stop
```

* ## Delete deployed Contracts
    ```bash
    $ tbears clear
    ```

# Trouble Shooting

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

When you receive an "put is not allowed" error, try this:
- Go to ```~/word/lib/python3.6/site-packages/iconservice/database/db.py```, ```_is_db_writable_on_context()```.
- Change the following code

    ```python
        return context_type != IconScoreContextType.QUERY and \
            func_type != IconScoreFuncType.READONLY
    ```

    to

    ```python
        return True
    ```
