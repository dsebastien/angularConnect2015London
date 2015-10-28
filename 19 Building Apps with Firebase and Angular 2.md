# Building Apps with Firebase and Angular 2

## About Firebase
* Owned by Google
* NoSQL JSON database
* every piece of data is available via an URL
* has an SDK
* user authentication baked in
* live database
  * any client connected to the application will see changes to the data as it happens in real-time

## Connecting to Firebase using their SDK

```
// create a Firebase database reference
var ref = new Firebase("https://angular-connect.firebaseio.com");

// save data
ref.set("Hello Angular Connect!");

// sync data
ref.on("value", function(snapshot) {
    console.log(snapshot.val()); // snapshot of the data at this point in time
});

//
ref.push("Hello!"); // the data receives a timestamp-based unique id
```

## Integrates nicely with Angular 2
Thanks to:
* Zones
* Observables
* Pipes

## Example Firebase Pipe
```
template: `
    <li *ng-for="#key of firebaseUrl | firebaseevent:'child_added'">
        {{ key }}
    </li>
`
```

Steps:
* Create a Firebase ref inside the pipe
* Stream data from Firebase
* All handled in the template
