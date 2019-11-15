<h2>Angular guide with the main features.</h2>

<h3>Component Communication<h3>
  
<h4>PARENT -> CHILD</h4>

parent.component.ts  
```javascript
parentElements = [{type:'server',name:'TestServer',content:'Just a Test!'}];
```

parent.component.html  
```javascript
<app-child  [childElement]="parentElements"></app-child>
```

child.component.ts
```javascript
@Input() childElement:{type: string, name:string, content: string}
```

------------------------------------------------------------------------------
<h4>PARENT HTML -> CHILD HTML (Projecting content)</h4> 
OBS: If you want to access the value in child.component.ts, see ContentChild in this guide.

parent.component.html  
```javascript
<app-child> <p>This will be shown in the HTML of the clild.component</p> </app-child>
```

child.component.html
```javascript
<ng-content></ng-content> <!-- Everything inner the app-child tag will be shown here   -->
```
------------------------------------------------------------------------------
<h4>CHILD -> PARENT</h4>

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

<h4>Lifecycles<h4>
  
ngOnChanges --->  Called after a bound input property changes

ngOnInit ---> Called once the component is initialized

ngDoCheck --->  Called during every change detection run

ngAfterContentInit --->  Called after content (ng-content) has been projected into view

ngAfterContentChecked --->  Called every time the projected content has been checked

ngAfterViewInit --->  Called after the component’s view (and child views) has been initialize

ngAfterViewChecked --->  Called every time the view (and child views) have been checked

ngOnDestroy ---> Called once the component is about to be destroyed

------------------------------------------------------------------------------

<h4>ViewChild and ContentChild</h4>

#ViewChild - Light DOM

child.component.html
```javascript
<p #text> This will be in child.componente.ts</p>
```

child.component.ts
```javascript
@ViewChild('text', {static: true}) text: ElementRef;

ngAfterViewInit(){
  console.log(this.text); //This will be in child.componente.ts
}
```
------------------------------------------------------------------------------
#ContentChild - Shadow DOM

parent.component.html  
```javascript
<app-child> <p #text> This will be in child.componente.ts</p> </app-child>
```

child.component.html
```javascript
<ng-content></ng-content> <!-- Everything inner the app-child tag will be shown here   -->
```

child.component.ts
```javascript
@ContentChild('text', {static: true}) text: ElementRef;

ngAfterViewInit(){
  console.log(this.text); //This will be in child.componente.ts
}

```
------------------------------------------------------------------------------
<h4>Directives</h4>

*FOR
```javascript
 <div *ngFor="let item of items; let i = index"></div>
```
------------------------------------------------------------------------------
*IF
```javascript
 <div *ngIf="condition"></div>
```
------------------------------------------------------------------------------
* SWITCH
```javascript
 <div [ngSwitch]="value">
    <p *ngSwitchCase="5">Value is 5</p>
    <p *ngSwitchCase="10">Value is 10</p>
    <p *ngSwitchCase="100">Value is 100</p>
    <p *ngSwitchDefault>Value is Default</p>
</div>
```
------------------------------------------------------------------------------
* CUSTOM DIRECTIVE (This directive changes the color of the p element)

highlight.directive.ts
```javascript
import {Directive,Renderer2,OnInit,ElementRef,HostListener,HostBinding,Input} from '@angular/core';
@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective implements OnInit {

  @Input() defaultColor: string; //receives the yellow color
  @Input() highlightColor: string; //receives the red color 
  @HostBinding('style.backgroundColor') backgroundColor: string; //atribute selector we want to change
 
  constructor(private elRef: ElementRef, private renderer: Renderer2) { }
  
  ngOnInit() {
    this.backgroundColor = this.defaultColor; //initiate with defaulColor
  }
  @HostListener('mouseenter') mouseover(eventData: Event) { //activate when mouse is over 
    this.backgroundColor = this.highlightColor;
  }
  @HostListener('mouseleave') mouseleave(eventData: Event) { //activate when mouse leave 
    this.backgroundColor = this.defaultColor;
  }
}
```
app.component.html
```javascript
<p appHighlight  defaultColor="yellow" highlightColor="Red">Style me with a better directive!</p>
```
------------------------------------------------------------------------------
* CUSTOM DIRECTIVE (This directive hides elements)

unless.directive.ts
```javascript
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';
@Directive({
  selector: '[appUnless]'
})
export class UnlessDirective {
  @Input() set appUnless(condition: boolean) { //create the name of the Directive
    if (condition) {
      this.vcRef.createEmbeddedView(this.templateRef); //Show the elements
    } else {
      this.vcRef.clear(); //Hide the elements
    }
  }
  constructor(private templateRef: TemplateRef<any>, private vcRef: ViewContainerRef) { }
}

```
app.component.html
```javascript
 <div *appUnless="condition">
   <p>Show if condition is True</p>
 </div>
```
