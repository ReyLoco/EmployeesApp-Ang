# EmployeesApp.

Aplicación para el aprendizaje de Angular. Se trata de una simple aplicación CRUD para la gestión de empleados.

## Desarrollo y progreso de la aplicación.

Se expone aquí el proceso y desarrollo realizado para la creación de la aplicación. Como se trata de una de las primeras aplicaciónes que desarrollo en Angular, describo aquí todos los pasos realizados.

### Creacion Employees App.

Crear una carpeta dónde se generarán todos los archivos, y abrir una consola de comandos.

`raiz> ng new employees-app`

Seleccionar durante el proceso de creación:

- Strict TypeScript: N
- Routes: Y
- CSS: scss

### Arrancar la aplicación en el servidor localhost.

`raiz>cd raiz/employees-app`
`raiz/employees-app> ng serve -o`

### En **app.component.html**.

Eliminar todo el código y aAñadir Divs con el router.

```
<div class="container">
  <div class="row">
    <div class="col-md-12">
      <router-outlet></router-outlet>
    </div>
  </div>
</div>
```

### Instalar Bootswatch.

Utilizaremos Bootswatch para aplicar de forma fácil temas y colores al desarrollo. Se trata de un package que utiliza Bootstrap "por debajo".

`raiz/employees-app>npm install bootswatch bootstrap jquery @popperjs/core`

### Seleccionar Theme.

En https://bootswatch.com/ escojer un theme para el desarrollo.

En **styles.css** (del raiz) y copiar de https://www.npmjs.com/package/bootswatch
los imports cambiando el nombre del theme de las cadenas.

```
  @import "~bootswatch/dist/[theme]/variables";
  @import "~bootstrap/scss/bootstrap";
  @import "~bootswatch/dist/[theme]/bootswatch";
```

En _angular.json_ añadir los scripts de los imports.

```
  "scripts": [
    "node**modules/jquery/dist/jquery.min.js",
    "node**modules/@popperjs/core/dist/umd/popper.min.js",
    "node**modules/bootstrap/dist/js/bootstrap.min.js"
  ]
```

### Crear componente header con su módulo.

`raiz/employees-app>ng g c shared/components/header --module app --skip-tests`
`raiz/employees-app>ng g m shared/components/header --module app`

### Crear nav.

- En https://bootswatch.com/ seleccionar y copiar una plantilla para el nav.
- Pegar el código en **header.component.html**.
- Modificar el nav para dejar opciones necesarias.
- Cambiar los href por [routerLink]="['/enlace']" con la opción de menú correspondiente.

### Crear módulos para las páginas.

Con el param --route List, creará el componente para cada page.

```
`raiz/employees-app> ng g m pages/employees/list --module app --route list`
`raiz/employees-app> ng g m pages/employees/new --module app --route new`
`raiz/employees-app> ng g m pages/employees/details --module app --route details`
`raiz/employees-app> ng g m pages/employees/edit --module app --route edit`
```

### Crear un Servicio para las llamadas a bd.

`raiz/employees-app> ng g s pages/employees/employees --module app --route edit --skip-tests`

### Desarrollo de la página List.

En **list.component.html**.

- Seleccionar y añadir una tabla de las plantillas de Bootswatch.
- Envolver en un div `class="table-responsive"`.
- Dejar un sólo **TR**.
- Añadir o quitar **TH** según las columnas necesarias.
- En la **TR** dejar la `class="table-info"` o la que queramos según color elegido.
- En la TR añadir una directiva *ngFor="let item from employess" o *ngFor="let item of [0,1,2,3,4]" para mock.
- Añadir Botones para las actions (seleccionar plantilla en Bootswatch) dentro del **TR** debajo de los **TD**, dentro de otro **TD**.
- Modificar valores de children de cabeceras, botones y mock de datos.
- Añadir un **TD** para los botones/actions `<td class="btn-group d-none d-sm-block" role="group">`.
- Añadir `class="d-none d-sm-block"` al **TH** de las actions para que se oculten los botones en modo móvil.
- Añadir función para el evento click.

En el **List.components.ts**

- Importar Router.
- Añadir Router en los parámetros del constructor.
- Crear los métodos para los botones:

  ```
  onGoToEdit(item: any): void {
    this.router.navigate(['edit']);
  }

  onGoToShow(item: any): void {
    this.router.navigate(['details']);
  }

  onGoToDelete(item: any): void {
    console.log('deleted');
  }
  ```

- Añadir NavigationExtras para la comunicación de valores entre los componentes/paginas.
