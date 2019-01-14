## Introduction

This is reproduction for https://github.com/prisma/prisma/issues/3811

## Steps for Reproduction

1. Deploy to model to local container
2. Run these to get some data:

```graphql
mutation {
  createOrganisation(
    data: { name: "Prisma", user: { create: { name: "Harshit" } } }
  ) {
    id
  }
}
```

3. Now query this data and grab the ids for next step:

```graphql
{
  users {
    id
    organisations {
      name
      id
    }
  }
}
```

4. Execute this (replace ids)

```graphql
mutation {
  updateUser(
    data: {
      organisations: {
        disconnect: { id: "cjqwhotlv000c0907wkcjp1l7" }
        updateMany: {
          where: { id: "cjqwhotlv000c0907wkcjp1l7" }
          data: { name: "Jsaf" }
        }
      }
    }
    where: { id: "cjqwhotnm000d0907vhvmf0pr" }
  ) {
    id
  }
}
```
