# Integration and End-to-end Tests with Node.js and MongoDB

## Introduction

In this article, you will learn how to write integration and end-to-end tests easily for your Node.js and MongoDB application that run on real instances of the database all without needing to set up an elaborate environment or complicated setup/teardown code.

You will see how the mongo-unit package helps with integration and end-to-end testing in Node.js. For a more comprehensive overview of Node.js integration tests, see this [article].

## Mongo-Unit

[Mongo-unit] is a Node.js package that can be installed using NPM or Yarn. It runs MongoDB in-memory. It makes integration tests easy by integrating well with Mocha and providing a simple API to manage the database state.

The library uses the mongodb-prebuilt NPM package, which contains prebuilt MongoDB binaries for the popular operating systems. These MongoDB instances can run in in-memory mode.

To add mongo-unit to your project, you can run:

    npm install -D mongo-unit

## Using Mongo-unit for Integration Tests
```javascript
// service.js
const mongoose = require('mongoose')
const mongoUrl = process.env.MONGO_URL || 'mongodb://localhost:27017/example'
mongoose.connect(mongoUrl)
const TaskSchema = new mongoose.Schema({
 name: String,
 started: Date,
 completed: Boolean,
})
const Task = mongoose.model('tasks', TaskSchema)

module.exports = {
 getTasks: () => Task.find(),
 addTask: data => new Task(data).save(),
 deleteTask: taskId => Task.findByIdAndRemove(taskId)
}
```

```javascript
// server.js
const express = require('express')
const bodyParser = require('body-parser')
const service = require('./service')
const app = express()
app.use(bodyParser.json())

app.use(express.static(`${__dirname}/static`))
app.get('/example', (req, res) => {
 service.getTasks().then(tasks => res.json(tasks))
})
app.post('/example', (req, res) => {
 service.addTask(req.body).then(data => res.json(data))
})
app.delete('/example/:taskId', (req, res) => {
 service.deleteTask(req.params.taskId).then(data => res.json(data))
})
app.listen(3000, () => console.log('started on port 3000'))
```

```javascript
// test-helper.js (mocha.js)
const prepare = require('mocha-prepare')
const mongoUnit = require('mongo-unit')

prepare(done => mongoUnit.start()
 .then(testMongoUrl => {
   process.env.MONGO_URL = testMongoUrl
   done()
 }))
```

```json
// testData.json
{
   "tasks": [
   {
     "name": "test",
     "started": "2017-08-28T16:07:38.268Z",
     "completed": false
   }
 ]
}
```

```javascript
// service.test.js
const expect = require('chai').expect
const mongoose = require('mongoose')
const mongoUnit = require('mongo-unit')
const service = require('./app/service')
const testMongoUrl = process.env.MONGO_URL

describe('service', () => {
 const testData = require('./fixtures/testData.json')
 beforeEach(() => mongoUnit.initDb(testMongoUrl, testData))
 afterEach(() => mongoUnit.drop())

 it('should find all tasks', () => {
   return service.getTasks()
     .then(tasks => {
       expect(tasks.length).to.equal(1)
       expect(tasks[0].name).to.equal('test')
     })
 })

 it('should create new task', () => {
   return service.addTask({ name: 'next', completed: false })
     .then(task => {
       expect(task.name).to.equal('next')
       expect(task.completed).to.equal(false)
     })
     .then(() => service.getTasks())
     .then(tasks => {
       expect(tasks.length).to.equal(2)
       expect(tasks[1].name).to.equal('next')
     })
 })

 it('should remove task', () => {
   return service.getTasks()
     .then(tasks => tasks[0]._id)
     .then(taskId => service.deleteTask(taskId))
     .then(() => service.getTasks())
     .then(tasks => {
       expect(tasks.length).to.equal(0)
     })
 })
})
```

## References
[Integration and End-to-end Tests with Node.js and MongoDB](https://www.toptal.com/nodejs/integration-and-e2e-tests-nodejs-mongodb)
[mongo-unit](https://github.com/mikhail-angelov/mongo-unit)
[Mockgoose](https://github.com/mockgoose/mockgoose)
[article](https://www.toptal.com/nodejs/nodejs-guide-integration-tests)