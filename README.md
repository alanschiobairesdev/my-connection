# pg-connection
Simple PotgreSQL wrapper for nodejs, to simplify its development.

WIP


## Install
``npm install @schirrel/pg-connection --save``


### Config
Uses `.env`  to aquire credentials.
|Prop|Required| Default | Description |
| ------------ | ------------ | ------------ | ------------ |
|CON_USER| Required | | |
|CON_URL| Required |  | |
|CON_DATABASE |Required  | | |
|CON_PASSWORD |Required  | | |
|CON_PORT | Optional |3306 | |
|CON_SSL | Optional |false | |
|CON_REJECT_UNHAUTHORIZED | Optional | | |
|CON_LOG | Optional |false | |
| CON_LIMIT| Optional |10 | |


## Usage

Using in 3 Steps

1. .env


```
CON_USER=postgres
CON_URL=localhost
CON_DATABASE=postgres
CON_PASSWORD=postgres
CON_SCHEMA=mercado_alencar
CON_LOG=true
```

2. Model
```javascript
const Model = require('@schirrel/pg-connection/Model');
class User extends Model{
	constructor(args = {}){
	super("USER");
	this.addColumn('email', 'EMAIL');
	this.addColumn('name', 'NAME');
	this.addColumn('password', 'PASSWORD');
	this.addColumn('active', 'ACTIVE', true);
	this.setValues(args);
	}
}

module.exports = User;
```

3. Repository
```javascript
const Repository = require('@schirrel/pg-connection/Repository');
const User = require('../models/User');

class UserRepository extends Repository{
	constructor(){
		super(User);
	}
}

module.exports = UserRepository;
```

And thats it.


## TL;DR
### Model
- Used as `extends Model` at your model class
- Call `super("TABLE_NAME")` with your table name 
- To add a columns `this.addColumn('email', 'EMAIL');`, it accepts a 3rd parameter as the default value.
- To set values of your constructor use ``this.setValues(args);`` 


### Repository
- Used as `extends Repository` at your repo class
- Call `super(YourClass);` with your class reference
- it already have built in: get(id), create(model), update(model),delete(id), list(), search(options)
