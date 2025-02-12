## Python requests module

### Difference between data and json

**json** : It automatically sets Content-Type header to “application/json” and converts provided data into JSON string.

**data** : It allows us to send data in the form of a dictionary, bytes, or file-like object. We should set ‘Content-Type’ explicitly while using data.

So the difference b/w both is how Content-Type is being set.

```python
response = requests.post(url=url, json=request_body)

print(response.status_code, response.json()) 

# 201 {'title': 'new_blog', 'body': 'new_blog is new blog', 'userId': 1, 'id': 101}
```

```python 
response = requests.post(url=url, json=request_body)

# can be replaced with 

response = requests.post(url, data=request_body) 

```
