# Different ways to test/debug shopify theme code
## a.  Use {{ debug }} outputs
Add temporary debug statements to output values. This helps you inspect variables and objects at runtime. for objects use `json` filter like `{{product | json}}`

Examples:
```liquid
{{ product.title }}
{{ cart | json }}
{{ block.settings | json }}

```
You can combine capture and `<pre>`, and wrap debug data in `<pre>` tag for formatting
like
```liquid
{% capture debug_output %}
  {{ product | json }}
{% endcapture %}

<pre>{{ debug_output }}</pre>
```
## b. Comment out chunks of Liquid logic to isolate issues
Example:
```liquid
{% comment %}
  {% if some_var %}
    ...some code...
  {% endif %}
{% endcomment %}

```
## c. Check Developer Console (DevTools)
Inspect the rendered HTML to see if the Liquid output matches your expectations (especially useful for checking CSS classes or dynamic content).

## d. Use  `Shopify theme check` command
You can use `shopify theme check` command if you are working on local in VS code or other editor, errors will be shown in the terminal

## e. Log Liquid data to HTML comments
If you don't want to expose debug output visually, write to HTML comments
Example: 
```liquid
<!-- Product: {{ product | json }} -->

```
OR
You can use script tag to print response in browser console like:
```javascript
<script>
console.log({{product | json}});
</script>
```
## f. Use Control Variables for Debug Mode
You can set a hardcoded variable or theme setting like `settings.debug_mode` to toggle debug mode
```liquid
{%- assign debug_mode = true -%}
{% if debug_mode %}
  {{ product | json }}
{% endif %}

```
## g. Check explicitly for `empty` and `blank` conditions
For strings, you can check for blank and for objects you can use empty.

In case of draft prodct
```liquid
{% if product %}
 <!-- Access product data here -->
{% endif %}
```
it will return true even if product is not available, so for objects like product use empty check
like
```liquid
{% if product != empty %}
     <!-- Access product data here -->
{% endif %}

OR
{% if product.id != blank %}
     <!-- Access product data here -->
{% endif %}
```

 # REST Vs GraphQL API

 | Feature            | REST                                                               | GraphQL                                              |
| ------------------ | ------------------------------------------------------------------ | ---------------------------------------------------- |
| **Definition**     | APIs using multiple endpoints & HTTP verbs | Query language for APIs using a single endpoint      |
| **Endpoints**      | Multiple (e.g., `/users`, `/orders`)                               | Single (e.g., `/graphql` or `graphql.json`)                            |
| **Data Fetching**  | Over-fetching & under-fetching possible                            | Client requests exactly the needed fields            |
| **HTTP Methods**   | GET, POST, PUT, PATCH, DELETE                                      | Usually POST (GET possible for queries)              |
| **Versioning**     | `/v1/`, `/v2/` in URLs                                             | Schema evolution without versioning                  |
| **Performance**    | Multiple round trips for related data                              | Single request for nested data                       |
| **Rate Limiting**  | Count-based limits (req/min)                                       | Complexity-based limits (query cost, usually in points based on Leaky Bucket algorithm)                 |
| **Error Handling** | Uses HTTP status codes (404, 500)                                  | Always `200 OK` + `errors` array in JSON             |
| **Caching**        | Simple with HTTP headers                                           | More complex; needs persisted queries/client caching |
| **Learning Curve** | Easier for beginners                                               | Requires learning schema, resolvers, query syntax    |
