# Deploy

```
tbears deploy -k keys/1/private.key -c contracts/irc2_token/sampletoken.json contracts/irc2_token/sample_token
```

Get "scoreAddress" by ```tbears txresult {the above TxID}```.
- For example: ```cxc083078edbe951560728105235c235d6f5906c65```


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
