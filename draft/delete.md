## Delete a page

To delete a previously created page, call the endpoint  `PUT /pages/{slug}/cancel`

### Example

- `jwt` token is `xxx`
- page slug (id) is `mdaricout-ex43r`

```curl
curl -X PUT 'https://api.inmemori-dev.com/pages/mdaricout-ex43r/cancel' \
  -H 'authorization: JWT xxx'
```
