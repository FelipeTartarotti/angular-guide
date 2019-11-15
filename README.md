<h3>Angular guide with the main features.</h3>
<h4>Component Communication<h4>

* Parent -> Child 

app.component.ts
```
export class AppComponent {
  serverElements = [{type:'server',name:'TestServer',content:'Just a Test!'}];
}
```
app.component.html
```
<app-server-element  [element]="serverElements"></app-server-element>
```

