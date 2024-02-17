# Angular lifecycle

En este articulo vamos a ver el ciclo de vida de Angular. es solamente para recordar como funciona Angular y como podemos utilizarlo para nuestro beneficio.

## Lifecycle hooks

Angular nos provee de varios hooks que podemos utilizar para realizar acciones en diferentes momentos del ciclo de vida de un componente.

```typescript
import { Component, OnInit, OnChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy } from '@angular/core';
```

### OnInit

Este hook se ejecuta una vez que el componente ha sido inicializado.

```typescript
ngOnInit() {
  console.log('Componente inicializado');
}
```

Es importante saber que se ejecuta al ser inicializado, pero no necesariamente cuando el componente ha sido renderizado en el DOM.
Si necesitamos realizar acciones despues podemos utilizar el hook `ngAfterViewInit`.

Siguiendo las mejores prácticas de Angular, es recomendable realizar las acciones en el hook `ngOnInit` y no en el constructor.
A su vez tambien tenemos las siguientes recomendaciones al usar este hook

- No realizar peticiones HTTP
- No realizar acciones que puedan afectar el DOM

Entre algunas restricciones en seguridad que podemos tener al utilizar este hook, es que no podemos acceder a los elementos del DOM, ya que estos no han sido renderizados. Se recomienda utilizar el hook `ngAfterViewInit` para realizar acciones que requieran acceder al DOM.

No olviden importar el hook en el componente y agregarlo al componente

### onChanges

ngOnChanges es uno de los hooks del ciclo de vida de un componente en Angular. Este hook se ejecuta cada vez que Angular detecta un cambio en las propiedades del componente.

```typescript
import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';

@Component({
  selector: 'my-component',
  template: `<h1>{{name}}</h1>`
})
export class MyComponent implements OnChanges {
  @Input() name: string;

  ngOnChanges(changes: SimpleChanges) {
    for (let propName in changes) {
      let change = changes[propName];
      let curVal  = JSON.stringify(change.currentValue);
      let prevVal = JSON.stringify(change.previousValue);
      console.log(`propName = ${propName}, currentValue = ${curVal}, previousValue = ${prevVal}`);
    }
  }
}
```

`ngOnChanges` se ejecuta antes de ngOnInit, es importante tenerlo en cuenta.

### DoCheck

### AfterContentInit

### AfterContentChecked

### AfterViewInit

### AfterViewChecked

### OnDestroy

## Secuencia de ejecucion Lifecycle

La ejecucion de los hooks se realiza en el siguiente orden:

1. ngOnChanges
2. ngOnInit
3. ngDoCheck
4. ngAfterContentInit
5. ngAfterContentChecked
6. ngAfterViewInit
7. ngAfterViewChecked
8. ngOnDestroy

## Conclusiones

Entender el ciclo de vida de Angular es muy util para realizar acciones en diferentes momentos de un componente. Es recomendable tenerlos en cuenta en nuestro desarrollo.
