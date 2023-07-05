# How we javascript

Javascript has been around since the beginning of the internet and has evolved massively as a language. There are therefore many flavours of javascript one could write. Here are some of the approaches we take to make working with shared code bases easier.

# 1. Modules rather than CommonJS

There are two ways you can use code from other files in Node. The traditional way is called CommonJS. It is being replaced by the more modern Module syntax.

## Example CommonJS syntax
```
const moment = require('moment')

exports.CONSTANT = 'I am a constant'
exports.func = () => {}
```

## Example Module 
```
import moment from 'moment'
import { namedImport } from 'somewhere'

export const CONSTANT = 'I am a constant'
const func = () => {}
export default func
```

Wherever possible we use the Module syntax.



## Questions
If you have any questions about this process, reach out to andi@wakeflow.io

