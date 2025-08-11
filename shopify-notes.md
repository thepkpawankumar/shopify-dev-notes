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
