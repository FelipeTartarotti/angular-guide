<h2>Angular guide with the main features.</h2>

<h3>Component Communication<h3>


* <h4>PARENT -> CHILD</h4>

parent.component.ts  
```javascript
parentElements = [{type:'server',name:'TestServer',content:'Just a Test!'}];
```

parent.component.html  
```javascript
<app-child  [childElement]="parentElements"></app-child>
```

clild.component.ts
```javascript
@Input() childElement:{type: string, name:string, content: string}
```

------------------------------------------------------------------------------
* <h4>PARENT HTML -> CHILD HTML (Projecting content)</h4> 

parent.component.html  
```javascript
<app-child> <p>This will be shown in the HTML of the clild.component</p> </app-child>
```

clild.component.html
```javascript
<ng-content></ng-content> <!-- Everything inner the app-child tag will be shown here   -->
```
------------------------------------------------------------------------------
* <h4>CHILD -> PARENT</h4>


child.component.ts
```javascript
@Output() childElement = new EventEmitter<{name:string, surname:string}>();

this.childElement.emit({
  name: 'Felipe',
  surname: 'Tartarotti'
});

```
parent.component.html
```javascript
<app-cockpit (childElement)="parentReceives($event)"></app-cockpit>
```

parent.component.ts
```javascript

parentReceives(personData:{name:string, surname:string}) {
  console.log('Name': personData.name);
  console.log('Surname': personData.surname);
}
  
```
------------------------------------------------------------------------------

<h3>Lifecycles<h3>
  
ngOnChanges --->  Called after a bound input property changes

ngOnInit ---> Called once the component is initialized

ngDoCheck --->  Called during every change detection run

ngAfterContentInit --->  Called after content (ng-content) has been projected into view

ngAfterContentChecked --->  Called every time the projected content has been checked

ngAfterViewInit --->  Called after the component’s view (and child views) has been initialize

ngAfterViewChecked --->  Called every time the view (and child views) have been checked

ngOnDestroy ---> Called once the component is about to be destroyed

------------------------------------------------------------------------------


