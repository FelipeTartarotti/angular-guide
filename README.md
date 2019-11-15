<h3>Angular guide with the main features.</h3>
<h4>Component Communication<h4>

* Parent -> Child 

parent.component.ts  
```angular
serverElements = [{type:'server',name:'TestServer',content:'Just a Test!'}];
```

parent.component.html  
```angular
<app-server-element  [element]="serverElements"></app-server-element>
```

clild.component.ts
```angular
@Input() element:{type: string, name:string, content: string}
```
