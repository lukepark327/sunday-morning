# Deploy

```
tbears deploy -k keys/1/private.key -c contracts/irc2_token/sampletoken.json contracts/irc2_token/sample_token
```


## Trouble Shooting

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
