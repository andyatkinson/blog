---
layout: post
title: "Encrypting and decrypting with Ruby"
date: 2018-01-22 13:00
comments: true
categories: [Ruby, Tips]
---

For a recent project I had the opportunity to research how we might encrypt a few pieces of data, with a shared key and initial value, and I put together the following notes. This is mostly re-hashing the [OpenSSL:Cipher documentation](https://ruby-doc.org/stdlib-1.9.3/libdoc/openssl/rdoc/OpenSSL/Cipher.html) if you'd rather jump straight there.

In this example we'll represent some fields of data about a person as a Ruby Hash that maps the name of the data to the value. Let's say we are storing their name, email, and date they were created.

### Encrypt

In addition to encrypting the data, we will convert it to JSON for easier serialization and deserialization, URL encode it to handle tricky characters like spaces, and base64 encode it to shrink it down.

In the example below, a random key and initial value are generated and assigned, and the variable is assumed to be accessible in the decryption step. This would be the case in a Ruby IRB session for example, but in a real world scenario you'd store these values somewhere else.

```
data = {:name=>"Andy A.", :email=>"andy+hello@example.com", :created_on=>"2018-01-20"}.stringify_keys

require 'openssl'
require 'uri'
require 'base64'
require 'json'

cipher = OpenSSL::Cipher::AES.new(256, :CBC)
cipher.encrypt

key = cipher.random_key
iv = cipher.random_iv

encrypted = cipher.update(data.to_json) + cipher.final

encoded = URI::encode(Base64.encode64(encrypted))
```

Now we have an encoded and encrypted representation to store.


### Decrypt

```
decipher = OpenSSL::Cipher::AES.new(256, :CBC)
decipher.decrypt
decipher.key = key
decipher.iv = iv

plain = decipher.update(encrypted) + decipher.final
data == JSON.parse(plain)
```

We reverse this process to decipher, generating a plan text version, and then de-serializing the JSON string, to end up with the same Ruby hash of person attributes!
