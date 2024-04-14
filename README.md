# WebEx API Calls

## Use the "max" query parameter to pull x objects from the API. 
### If the response includes a "link" header, more objects exist on the target API endpoint.
### Subsequent calls can be made to pull the rest of the objects.
```
❯ curl -s -i -k -H "Authorization: Bearer $ACCESS_TOKEN" 'https://webexapis.com/v1/teams?max=2' | grep link
link: <https://webexapis.com/v1/teams?max=2&cursor=xxxxxxxxxxxxxxxx>; rel="next"

❯ curl -s -k -H "Authorization: Bearer $ACCESS_TOKEN" 'https://webexapis.com/v1/teams?max=2' | jq ".items[].name"
"TeamSpace_Demo1"
"TeamSpace_Demo2"
```

### Subsequent call using the link header from the previous call to pull the next x objects.
```
❯ curl -s -i -k -H "Authorization: Bearer $ACCESS_TOKEN" 'https://webexapis.com/v1/teams?max=2&cursor=xxxxxxxxxxxxxxxx' | grep link
link: <https://webexapis.com/v1/teams?max=2&cursor=xxxxxxxxxxxxxxx1>; rel="next"

❯ curl -s -k -H "Authorization: Bearer $ACCESS_TOKEN" 'https://webexapis.com/v1/teams?max=2&cursor=xxxxxxxxxxxxxxxx' | jq ".items[].name"
"TeamSpace_Demo3"
"TeamSpace_Demo4"
```






