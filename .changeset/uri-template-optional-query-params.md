---
"@modelcontextprotocol/core": patch
---

fix(core): make UriTemplate query parameters optional and order-independent

`UriTemplate.match()` now correctly handles `{?param1,param2,...}` and `{&param}` expressions per RFC 6570 §3.2.8:

- A URI with **no query parameters** matches a template with optional query params.
- A URI with a **subset** of the declared params matches (the rest are absent from the result).
- Params may appear in **any order** in the URI regardless of template declaration order.

Also stops simple-string variables (`{var}`) from greedily consuming `?` and `#` characters, which are RFC 3986 component delimiters that must not be captured by a path variable.

Fixes #1079.
