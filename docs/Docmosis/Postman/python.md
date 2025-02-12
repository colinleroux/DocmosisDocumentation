## Python requests module

### Difference between data and json

**json** : It automatically sets Content-Type header to “application/json” and converts provided data into JSON string.

**data** : It allows us to send data in the form of a dictionary, bytes, or file-like object. We should set ‘Content-Type’ explicitly while using data.

So the difference b/w both is how Content-Type is being set.