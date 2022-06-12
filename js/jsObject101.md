## Object
- key/value pairs/attributes
- can have nestable attributes (object values)
- can have list values
- can have function values

```javascript
{
    name: 'David',
    age: '40',
}

{
    name: 'Mike',
    address: {
        line1: 'B-06, Aurora Lane',
        city: 'Melbourne',
        country: 'AUS',
    }
}

{
    name: 'Tom',
    contacts: [{
        type: 'mobile',
        number: 123132213,
    }, {
        type: 'home',
        number: 12312313213,
    }]
}

{
    name: 'John',
    income: 10000,
    annualIncome: function() {
        return this.income * 12;
    },
}
```
This syntax is same as JSON.

### Init, Get & Set
```javascript
// Initialize
const person = {
    name: 'David',
    age: '40',
    gender: 'Male',
}

// Get
console.log(person);
console.log(person.name, person['age']);

const key = 'gender';
console.log(person.key);
console.log(person[key]);

// Set
person.name = 'David Thompson'; // overwriting
person.profession = 'Engineer'; // adding new attribute
person['income'] = 10000;
```

### Empty object
```javascript
const person = {};      // empty object
const person = null;    // empty-valued object
```
Both are kind of empty objects but where `{}` is used? To initialize an object and add attributes along the way.

```javascript
const person = {};
console.log(person);
console.log(person.age);

const person = null;
console.log(person);
console.log(person.age);

let person;
console.log(person);
console.log(person.age);
```

One thing you might have wondered so far. How can a constant value be assigned new attributes after initializing it?

              001f                            002f
             ------                         ---------
person1 =>   | {} |            person2 =>   | {...} |
             ------                         ---------

```javascript
const person1 = {};
const person2 = { name: 'Bob' };
person1 = person2;              // throws error
person1.name = person2.name     // valid
```

## Object clones

                    001f                      
             --------------------                        
person2 =>   | { name: '...',   |
             |   address: 00ff  |
             |                } |
             --------------------

             00ff                      
             --------------------                        
address =>   | { line1: '...',  |
             |   city: '...' }  |
             --------------------

### Shallow copy vs Deep copy
```javascript
const person2 = { name: 'Mike' };
const address = { country: 'AUS' };

person2.address = address;
console.log(person2);

// Shallow copy
const person1 = Object.assign({}, person2);
console.log('Person 1 after shallow copy: ', person1);

person2.name = 'Thomas';
address.country = 'USA';

console.log('Person 2 after updates', person2);
console.log('Person 1 after updates', person1);

// Deep copy
const person3 = JSON.parse(JSON.stringify(person2));

address.country = 'Canada';

console.log('Person 3 after updates', person3);
```
