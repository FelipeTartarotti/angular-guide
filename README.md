<h2>Angular guide with the main features.</h2>

:red_circle: <h3>Component Communication<h3>

:large_blue_circle:<h4>PARENT -> CHILD</h4>

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

<h4>CHILD -> PARENT<h4>
  
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


