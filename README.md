<h3>Angular guide with the main features.</h3>
<h4>Component Communication<h4>

*PARENT -> CHILD 

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
