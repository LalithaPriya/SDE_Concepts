## GraphQL

- a query language and alternative to standard request to rest API using end points.
- still uses HTTP under hood, but its more flexible to control 

- test.com/api/testpoint
- test.com/api/testpoint/123

This will handle the request to those endpoints aby connecting to db by fetching and sending or update or by delete

**Drawbacks**: 
- overfetching :
    - getting back more data than we need \
    Ex: test.com/api/courses --> this will fetch data related to.
    <pre>
        courses 
        {
            "id": "1",
            "title" : "graphQL",
            "author" : "me",
            "video" : "...",
            "length" : "...",
            "description" : "...",
            "price" : "..."
        }
    </pre>

    But, I wanna need few params in this case like id, desc and title. So we dont need any other details i.e overfetching

- underfetching:
    - getting back less data than we need \
     Ex: test.com/api/courses/2 --> this will fetch data related to course id 1.
     ```
        {
            "id": "1",
            "title" : "graphQL",
            "author" : {...},
            "video" : "...",
            "length" : "...",
            "description" : "...",
            "price" : "...",
            "url" : "..."
        }
    ```
    If we need to know more details about the author, we need to make additional request 
    test.com/api/author/me

This are easily solved by using GraphQL.

- It allows used to fecth the nested related  data with in a single query.

single Endpoint:

testGraphQL.com/graphql

```
Query{
    Courses{
        id,
        title,
        description
    }
}

Query{
    Course(id : "1"){
        id,
        title,
        description,
        author{
            name,
            id,
            Courses{
               id,
                title,
                description
            }
        }
    }
}
```
- We can also perform the mutations.
