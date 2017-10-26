# @jumpn/utils-graphql

> GraphQL utilities

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- END doctoc -->

- [Installation](#installation)
  - [Using npm](#using-npm)
  - [Using yarn](#using-yarn)
- [Types](#types)
- [API](#api)
  - [errorsToString](#errorstostring)
  - [getOperationType](#getoperationtype)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Installation

### Using [npm](https://docs.npmjs.com/cli/npm)

    $ npm install --save @jumpn/utils-graphql

### Using [yarn](https://yarnpkg.com)

    $ yarn add @jumpn/utils-graphql

## Types

```flowtype
type GqlErrorLocation = {
  line: number,
  column: number
};

type GqlError = {
  message: string,
  locations?: Array<GqlErrorLocation>
};

type GqlRequest<Variables: void | Object = void> = {
  operation: string,
  variables?: Variables
};

type GqlResponse<Data> = {
  data?: Data,
  errors?: Array<GqlError>
};

type GqlOperationType = "mutation" | "query" | "subscription";
```

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### errorsToString

Transforms an array of GqlError into a string.

**Parameters**

-   `gqlErrors` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;GqlError>** 

**Examples**

```javascript
const gqlRespose = {
  errors: [
    {message: "First Error", locations: [{column: 10, line: 2}]},
    {message: "Second Error", locations: [{column: 2, line: 4}]}
  ]
}

const error = errorsToString(gqlRespose.errors);
// string with the following:
// First Error (2:10)
// Second Error (4:2)
```

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

### getOperationType

Returns the type of the given operation

**Parameters**

-   `operation` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

**Examples**

```javascript
const operation = `
  subscription userSubscription($userId: ID!) {
    user(userId: $userId) {
      id
      name
    }
  }
`;

const operationType = getOperationType(operation);

console.log(operationType); // "subscription"
```

Returns **(void | GqlOperationType)** 

## License

[MIT](LICENSE.txt) :copyright: **Jumpn Limited** / Mauro Titimoli (mauro@jumpn.com)
