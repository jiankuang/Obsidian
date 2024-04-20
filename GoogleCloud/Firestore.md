Firestore is a NoSQL database with offline capability 
### Firestore & NoSQL Overview
#### Scaling 
* Vertically: Get beefier machines 
* Horizontally: Distributed across several machines 
#### SQL DB 
* PRO: Data integrity is high 
* CON: Complex queries can get slow 
* CON: Data structures are rigid and can force you into queries 
* CON: Scaling SQL, means scaling vertically 
#### NoSQL DB
Prioritize Reads over Writes 
![[Rows vs Documents.png]]
### Retrieving & Writing Data
#### References 
```js
import { collection, doc, getFirestore } from 'firebase/firestore'

const firestore = getFirestore()
// users Collection Reference
const usersCol = collection(firestore, 'users')
// get a single user 
const userDoc = doc(firestore, 'users/david')
```
#### onSnapshot()
```js
import { onSnapshot } from 'firebase/firestore'

onSnapshot(userDoc, snapshot => {
	// this is one doc 
	console.log(snapshot)
	// this is the data 
	console.log(snapshot.data())
})

onSnapshot(usersCol, snapshot => {
	// this is an array of docs 
	console.log(snapshot)
	// you can iterate through and map what you need 
	console.log(snapshot.docs.map(d => d.data()))
})
```
#### setDoc() vs updateDoc()
`setDoc` can be used for new doc creation; for existing doc, it will overwrite the doc with new data. 
`updateDoc` can only be used for existing doc update, it will merge the doc with new data.  
Use `setDoc()` with a merge if you want to create new doc and update existing doc with merge. 
```js
const newDoc = doc(firestore, 'user/new_user_maybe')
setDoc(newDoc, { name: 'Darla' }, { merge: true })
```
#### deleteDoc()
```js
const davidDoc = doc(firestore, 'users/david_123')
deleteDoc(davidDoc)
```
#### Generating Ids

#### Don't trust local dates 
```js
const newDoc = doc(firestore, 'marathon_results/david_123')
// Imagine this runs automatically when a runner croess the finish line 
setDoc(newDoc, {
	name: David,
	// What if the end user computer has incorrect date ? 
	// finishedAt: new Date() // Something like: '5/1/2022 9:32:12 EDT'
	finishedAt: serverTimestamp()
})
```
#### increment()

#### One write per second
Firestore can only reliably handle 1 write per second on a document 
#### Document change types 
#### The offline mode 
```js
import { getFirestore, enableMultiTabIndexedDbPersistence } from 'firebase/firestore'
enableMultiTabIndexedDbPersistence(getFirestore())
```
#### Snapshot metadata
```js
onSnapshot(userDoc, snapshot => {
	console.log(snapshot.data())
	// First time: { name: "David" }
	// Second time: { name: "David!" }
	console.log(snapshot.metadata)
	// Very first time, data is loaded: 
	// { fromCache: false, hasPendingWrite: false }
	
    // Second time,data is updated locally: 
    // { fromCache: true, hasPendingWrite: true }
})

updateDoc(userDoc, { name: 'David!' })
```
### Querying 
#### Query types 
Cloud Firestore has two types of queires: simple and composite. 
#### Simple Queries 
```js
import { collection, query, where, limit, getFirestore } from 'firebase/firestore'

const db = getFirestore()
const expensesCol = collection(db, 'expenses')
const expensesQuery = query(
	expensesCol,
	where('cost', '>', 200),
	limit(100),
)
```
