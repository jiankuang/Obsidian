![[Traditional architecture.png]]
![[Firebase architecture.png]]

### Setup
#### Setup Local Emulator Environment 
`npx firebase init emulators` select the emulators you want to setup (auth, firestore, hosting)
`npx firebase emulators:start` start emulators 
`npx firebase hosting:channel:deploy staging` deploy app in staging env, so won't affect production. Link will expire in 7 days 

### Authentication 

### Security 
Rules must match at the document level (not collection level) 