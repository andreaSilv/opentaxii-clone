- github.com/eclecticiq/OpenTAXII/blob/master/docs/auth.rst
- https://github.com/eclecticiq/cabby/blob/master/docs/user.rst
- https://github.com/eclecticiq/cabby

# Run
1. Cloned Cabby
2. changed image to python alpine (for the shell)
3. add cabby container to OpenTAXII docker_compose network

# Test
## Pull
1. `wget --post-data 'username=test&password=test' http://examples-opentaxii-1:9000/management/auth`
2. `cat auth`
3. with the token, in cabby container 
```
taxii-poll \
--path http://examples-opentaxii-1:9000/services/poll-a \
--collection collection-a \
--header Authorization:'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhY2NvdW50X2lkIjoxLCJleHAiOjE2Nzg5MTYyODJ9.UUwdfqNH3ySpYvFTXHGAdW9U1bsLJ781Z90_zC25iZ0'
```
## Push
1. `wget --post-data 'username=test&password=test' http://examples-opentaxii-1:9000/management/auth`
2. `cat auth`
3. with the token, in cabby container 
```
taxii-push \
--path http://examples-opentaxii-1:9000/services/inbox-a \
--dest collection-a \
--content-file /stuxnet.stix.xml \
--binding "urn:stix.mitre.org:xml:1.1.1" \
--subtype custom-subtype \
--header Authorization:'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhY2NvdW50X2lkIjoxLCJleHAiOjE2Nzg5MTYyODJ9.UUwdfqNH3ySpYvFTXHGAdW9U1bsLJ781Z90_zC25iZ0'

```

> `--content-file` [here](./examples/stix/stuxnet.stix.xml)

> `--container` in the push command must be set accordingly `--dest` in the pull