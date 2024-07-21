# Learning Laravel Lighthouse GraphQL

## Introduction

Laravel Lighthouse is a package that allows you to serve a GraphQL endpoint from your Laravel application. GraphQL provides a more efficient, powerful, and flexible alternative to REST. Lighthouse leverages the strengths of Laravel and GraphQL to create a seamless development experience.

## Table of Contents

- [Learning Laravel Lighthouse GraphQL](#learning-laravel-lighthouse-graphql)
  - [Introduction](#introduction)
  - [Table of Contents](#table-of-contents)
  - [Getting Started](#getting-started)
  - [Installation](#installation)
  - [Defining Schemas](#defining-schemas)
    - [Example Type Definition](#example-type-definition)
  - [Resolvers](#resolvers)
    - [Example Resolver](#example-resolver)
  - [Queries and Mutations](#queries-and-mutations)
    - [Example Query](#example-query)
    - [Example Mutation](#example-mutation)
  - [Relationships](#relationships)
    - [Example Relationship](#example-relationship)
  - [Middleware and Authorization](#middleware-and-authorization)
    - [Example Middleware Usage](#example-middleware-usage)
  - [Testing](#testing)
    - [Example Test](#example-test)
  - [Resources](#resources)

## Getting Started

Before diving into Laravel Lighthouse, ensure you have a basic understanding of Laravel and GraphQL. Familiarity with Laravel's Eloquent ORM, routing, and middleware will be beneficial.

## Installation

To get started with Laravel Lighthouse, you'll need to install the package via Composer.

```bash
composer require nuwave/lighthouse
```

After installation, publish the configuration file and schema:

```bash
php artisan vendor:publish --provider="Nuwave\Lighthouse\LighthouseServiceProvider" --tag=schema
```

## Defining Schemas

Schemas define the structure of your GraphQL API. In the `graphql/schema.graphql` file, you can define your types, queries, and mutations.

### Example Type Definition

```graphql
type User {
    id: ID!
    name: String!
    email: String!
}
```

## Resolvers

Resolvers handle the logic for fetching and manipulating data. You can define resolvers in your schema using directives.

### Example Resolver

```graphql
type Query {
    user(id: ID!): User @find
}
```

## Queries and Mutations

Queries are used to fetch data, while mutations are used to modify data.

### Example Query

```graphql
query {
    user(id: 1) {
        id
        name
        email
    }
}
```

### Example Mutation

```graphql
mutation {
    createUser(name: "John Doe", email: "john@example.com") {
        id
        name
        email
    }
}
```

## Relationships

Lighthouse makes it easy to define relationships between types.

### Example Relationship

```graphql
type Post {
    id: ID!
    title: String!
    content: String!
    user: User @belongsTo
}
```

## Middleware and Authorization

You can use middleware to handle authorization and other logic.

### Example Middleware Usage

```graphql
type Query {
    me: User @auth
}
```

## Testing

Testing your GraphQL API is crucial to ensure it works as expected. Lighthouse integrates well with Laravel's testing tools.

### Example Test

```php
public function testUserQuery()
{
    $user = User::factory()->create();

    $this->graphQL("
        query {
            user(id: {$user->id}) {
                id
                name
                email
            }
        }
    ")->assertJson([
        'data' => [
            'user' => [
                'id' => (string) $user->id,
                'name' => $user->name,
                'email' => $user->email,
            ],
        ],
    ]);
}
```

## Resources

- [Laravel Lighthouse Documentation](https://lighthouse-php.com/)
- [GraphQL Documentation](https://graphql.org/learn/)
- [Laravel Documentation](https://laravel.com/docs)

---

This markdown guide provides a structured overview of learning Laravel Lighthouse GraphQL. You can expand on each section with more detailed explanations and examples as you progress in your learning journey.
