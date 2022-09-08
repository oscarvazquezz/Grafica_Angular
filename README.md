# Graficar en Angular

Lo que se tiene que ser primero es instalar dos librerías en el proyecto de angular que son: 
   * npm install chart.js 
   * npm install ng2-charts
 
Luego se importa ChartsModule en el archivo app.module.ts.

```
import { ChartsModule } from 'ng2-charts';
@NgModule({
  declarations: [...],
  imports: [
    ChartsModule
  ],
  providers: [...],
  bootstrap: [...]
})
export class AppModule { }
```

Luego de importa ChartsModule en el proyecto ,ya puedes realizar las graficas que deseas usar.Un ejemplo seria: 
   * Grafica de barras

Para hacer la grafica de barras se realiza estos pasos:
   * Para el archivo de component.ts del componente de tu app se tiene que poner los datos que se necesita y importa las liberias que se usa chart.js y ng2-charts para graficar.
   
```
import { Component, OnInit } from '@angular/core';
import { ChartOptions, ChartType, ChartDataSets } from 'chart.js';
import { Label } from 'ng2-charts';

@Component({
  selector: 'app-grafica',
  templateUrl: './grafica.component.html',
  styleUrls: ['./grafica.component.css']
})

export class GraficaComponent implements OnInit {

  barChartOptions: ChartOptions = {
    responsive: true,
  };
  
  barChartLabels: Label[] = ['Apple', 'Banana', 'Kiwifruit', 'Blueberry', 'Orange', 'Grapes'];
  barChartType: ChartType = 'bar';
  barChartLegend = true;
  barChartPlugins = [];
  barChartData: ChartDataSets[] = [
    { data: [45, 37, 60, 70, 46, 33], label: 'Best Fruits' }
  ];
  

  constructor() { }

  ngOnInit(): void {
  }

}
```

  * Y para el archivo html del componente, se usa un canvas para graficar.En el componente canvas se envía los datos que se tiene que visualizar en la gráfica.
  
  ```
  <canvas baseChart 
    [datasets]="barChartData"
    [labels]="barChartLabels"
    [options]="barChartOptions"
    [plugins]="barChartPlugins"
    [legend]="barChartLegend"
    [chartType]="barChartType">
  </canvas>
  
  ```
  
Si todo va bien, entonces su resultado debe verse así.
  
  ![grafica](https://i.pinimg.com/originals/c8/fb/38/c8fb38a214579708cdb09e12200f8f56.jpg)

En caso que no se visualiza se tiene que exportar en la dirección del archivo Chart.min.js en el archivo angular.json.

```
"build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
            "outputPath": "dist/app",
            "index": "src/index.html",
            "main": "src/main.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "tsconfig.app.json",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "src/styles.css"
            ],
            "scripts": [
              "node_modules/chart.js/dist/Chart.min.js"
            ]
          },
   }
```

  
