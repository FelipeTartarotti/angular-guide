<h3>Angular guide with the main features.</h3>
<h4>Component Communication<h4>

* Parent -> Child 

parent.component.ts  
```javascript
serverElements = [{type:'server',name:'TestServer',content:'Just a Test!'}];
```

parent.component.html  
```javascript
<app-server-element  [element]="serverElements"></app-server-element>
```

clild.component.ts
```javascript
@Input() element:{type: string, name:string, content: string}
```
