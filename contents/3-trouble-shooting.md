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
