# ViraToken

Small lib to encode/decode/sign/verify JWTs using asymmetric cryptography.
Mostly a wrapper for [pyjwt](https://github.com/jpadilla/pyjwt/) for use with asymmetric cryptography.

It was made for an ecosystem of microservices. One microservice produces the tokens, and the others read them to get the username and stuff.


## Installing

```
$ pip install viratoken
```

## Usage

Having the private key you can encode and decode tokens:

```python
from viratoken import SignerVerifier

sv = SignerVerifier(priv_key_path="settings/key",
                    priv_key_password="settings/keypass")

# Token payload
token_data = {
    'username': 'bafafa',
    'more_data': 'rocambole',
}

# Token expiration time in minutes
exp_minutes = 60

encoded_token = sv.encode(token_data, exp_minutes)

decoded_token = sv.decode(encoded_token)
```

Having only the public key, you can only decode:

```python
sv = sv.config(pub_key_path="settings/keypub")
decoded_token = sv.decode(encoded_token)
```

You can also declare the `SignerVerifier` first and configure later:

```python
sv = SignerVerifier()
sv.config(priv_key_path="settings/key",
          priv_key_password="settings/keypass")
```
