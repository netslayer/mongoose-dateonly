#dateonly-mongoose

####Provides mongoose support for dates only, typically to avoid timezone issues.

##About

This is an implementation of the DateOnly library that works with Mongoose.  This allows you to save dates in Mongo without having to worry about time zones shifting the date.

##Usage

```javascript
var mongoose = require('mongoose');
var DateOnly = require('mongoose-dateonly')(mongoose);

var PersonSchema = {
  birthday: DateOnly
};

...

var p1 = new Person({ birthday: '4/7/1990' });
var p2 = new Person({ birthday: new Date('4/7/1990') });
var p3 = new Person({ birthday: new DateOnly('4/7/1999') });
```

In Mongo, the values above would all be stored as `19990307`.  Because they're not stored as conventional `Date` objects, they are not subject to time zone shifts.  In other words, no matter what time zone a user is in, this date will always be 4/7/1990.

The DateOnly data type supports all of the query conditions you would expect it to:

```
Person.find({ birthday: '4/7/1990' });
Person.find({ birthday: { $lt: Date.now() } });
Person.find({ birthday: { $in: [ '1/1/2000', new Date('1/1/2010'), new DateOnly()]}})
```

For full implementation details on the `DateOnly` data type, please see the documentation on the [https://github.com/boblauer/dateonly](DateOnly GitHub repo).

##Test
npm test
