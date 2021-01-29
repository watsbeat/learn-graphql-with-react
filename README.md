# Learning GraphQL

A code-along to Sections 1-5 of Udemy Course, ["GraphQL with React: The Complete Developer's Guide"](https://www.udemy.com/course/graphql-with-react-course/).

Some topics covered:

- Registering GraphQL with Express
- GraphQL Schemas
- Root Queries 
- Resolving with Data
- GraphiQL Tool
- Async Resolve Functions
- Nested Queries
- Multiple RootQuery Entry Points
- Bidirectional Relations
- Resolving Circular References with Closures
- Query Fragments
- Mutations & NonNull Fields

## Setup Instructions

1. `git clone git@github.com:watsbeat/learn-graphql-with-react.git` 
2. `cd learn-graphql-with-react`
3. `npm i` to install dependencies
4. `npm run json:server` to start the fake DB
5. `npm run dev` to start the express server (in a different terminal window)

## GraphiQL Queries:

Open `http://localhost:4000/graphql` in browser and try running:

_Note: Change any of the args passed to the queries as needed._

```graphql
query getUserById {
  user(id: "-gX5Pwb") {
    ...userDetails
  }
}

query getCompanyUsers {
  company(id: "2") {
    name
    description
    users {
      firstName
      company {
        description
      }
    }
  }
}

query getMultipleCompanies {
  apple: company(id: "1") {
    ...companyDetails
  }
  google: company(id: "2") {
    ...companyDetails
  }
}

fragment companyDetails on Company {
  id
  name
  description
}

fragment userDetails on User {
  id
  firstName
  age
  company {
    ...companyDetails
  }
}

mutation addNewUser {
  addUser(firstName: "Honor", age: 23) {
    ...userDetails
  }
}

mutation deleteUser {
  deleteUser(id: "-gX5Pwb") {
    id
  }
}

mutation editUser {
  editUser(id: "-gX5Pwb", firstName: "Jamie", age: 22, companyId: "2") {
    ...userDetails
  }
}
```
