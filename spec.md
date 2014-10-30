
Content-Hash URIs
-----------------

A content-hash URI is a URI which includes a secure hash of the content which is provided on dereference.  For example:

```bash
$ curl -o out http://www.w3.org/People/Sandro/content-hash=050b8ba1fe371df68f8bc8dbfb24ab40948256c2104ed475f62a7f3b287086db
$ sha256sum out
050b8ba1fe371df68f8bc8dbfb24ab40948256c2104ed475f62a7f3b287086db  out
```

A conforming content-hash client library is a Web client library which checks the content provided on dereference and rejects non-matching content.   Specifically, whenever the URI matches the regular expression `[?/&#]content-hash=[^/&#]*` the client library MUST return an error instead of the content, unless the content validates.  The content validates only if the secure hash of the returned content is the hash provided in the text of the URI.

For Version 1, the hash must be 64 lowercase hex digits and the hash algorithm is SHA-256.  Later versions may introduce other algorithms, indicated by the hash value being something other than 64 lowercase hex digits.   Client libraries SHOULD provide different errors for a non-version-1 content-hash URI and for a hash mismatch.

The headers are ignored in computing the hash.
