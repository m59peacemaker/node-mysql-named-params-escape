# MYSQL Named Params Escape

## Install
```
npm install mysql-named-params-escape
```

## Usage

```javascript
var npEscape = require('mysql-named-params-escape');
```

### Writing queries
```javascript
var query = "SELECT ::something FROM ::table WHERE ::table.::whatever = ::value";
var params = {
  something: 'title',
  table: 'foo',
  whatever: 'id',
  value: 123
};

// SELECT `title` FROM `foo` WHERE `foo`.`id` = 123;
```

### queryFormat

```javascript
connection.config.queryFormat = npEscape;

connection.query(query, params);
```

### Manual escaping

```javascript
query = npEscape(query, params);

connection.query(query);
```

### Parameters

#### query

Type: `String`

The string of MYSQL code to be escaped.
`::` followed by a word denotes an identifier to be escaped.
`:` followed by a word denotes a value to be escaped.

#### params

Type: `Object`

An object in which the keys correspond to placeholders in the query. The placeholders will be replaced with the values from the object.