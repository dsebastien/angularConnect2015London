# Building Apps with Firebase and Angular 2

## Links
* Code: https://github.com/sararob/angular2base
  * check out the Firebase pipe class

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

## Integrating Firebase and authentication

```
    // Firebase configuration
    firebaseUrl: string;
    firebaseRef:Firebase;
    isLoggedIn:boolean = false;
    authData: any;

    constructor() {
        console.log("Home component loaded");

        this.firebaseUrl = "http://myMediaManager.firebaseio.com"; // root
        this.firebaseRef = new Firebase(this.firebaseUrl);
        this.firebaseRef.onAuth((user) => {
            if(user){
                this.authData = user;
                this.isLoggedIn = true;
            }
        })
    }

    authenticateWithGoogle(){
        this.firebaseRef.authWithOAuthPopup("google", (error) => {
            if(error){
                console.log(error); // todo improve error handling
            }
        });
    }
```

With the above, the component connects to Firebase and we have a function to integrate Google authentication. All that is missing is something in the template to:
* trigger the authentication (Firebase will open a popup)
* react based on the isLoggedIn and authData variables

Example:
```
<button [hidden]="isLoggedIn" (click)="authWithGoogle()">
```

The above button will only be visible while the user is not logged in and will allow him to log in.

```
<input type="text" [hidden]="!isLoggedIn" (keyup)="doneTyping($event)" placeholder="Type something here" #messageText>
```

The above input box will only be displayed if the user is logged in.

```
<li *ng-for="#message of firebaseUrl | firebaseevent:'child_added'">
    {{message.name}}: {{message.text}}
</li>
```

## Firebase hosting
Applications can easily be deployed on the Firebase infrastructure:
* install firebase-tools globally
* add a firebase.json file in the folder: tells Firebase what should be deployed (e.g., dist folder)
* invoke `firebase deploy`
* invoke `firebase open`

## Upcoming
More expressiveness in templates:

```
<li *ng-for="firebase(url) | listen: childAdded | orderBy: firstName | startAt: 's' | limit: 10">
    {{user.firstName}}
</li>
```
