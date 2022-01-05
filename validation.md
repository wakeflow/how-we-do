# How we validate

In programming you often need to check that a variable has acceptable values.

E.g. You want to check that 
- a street name is no longer than 25 characters
- a phone number has only numbers and the + character
- an age is a number between 0 and 100 

# JSON-Schema

There are countless libraries out there that allow you to perform these checks. In order to make it easy for all the members of our team to work together, we therefore all use the same approach. This is called JSON-Schema.

JSON-Schema is a standard (rather than an individual library) that allows you to define what a variable looks like.

The definition of the schema is a JSON-object and can be stored in a .json file in a /schemas folder.

To familiarise yourself with the format that a JSON-Schema takes, please have a look at [json-schema.com](). TODO!!!!


# Example JSON-Schema
```
const schema = {
  type: 'object',
  required: [id,status],
  properties: {
    id: {
      type: 'integer',
      example: 123,
      minimum: 0,
      maximum: 10 ** 20
    },
    url: {
      type: 'string',
      maxLength: 255,
      example: 'https://mywebsite.com'
    },
    status: {
      type: 'string',
      enum: ['active','inactive'],
      example: 'active',
      default: 'active'
    },
  }
};

```

# Example Validation Code
```
const Validator = require('jsonschema').Validator;
const validator = new Validator();

const validateJsonSchema = (data,schema) => {
  const result = validator.validate(data,schema,{ nestedErrors: true });
  result.errors.forEach(error=>{
    console.log(error)
  });
};
```

## Questions
If you have any questions about this process, reach out to andi@wakeflow.io

