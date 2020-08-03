# density-plot

## Overview
This function (`processDensity()`) allows you to create a density chart using [Highcharts](https://www.highcharts.com/): 

*Check [codePen demo](https://codepen.io/mushigh/pen/wvMVMma)*


![Density](img/density.png)


## Installation
You can either add the function direclty in your code (see [density-plot.js](density-plot.js)) or use the following [link](https://marketing-demo.s3-eu-west-1.amazonaws.com/densityFunction/processDensity.js) (see below):
````
<script src="https://marketing-demo.s3-eu-west-1.amazonaws.com/densityFunction/processDensity.js"></script>
````

## Description
Here is the description of the function’s parameters:
* **step** is the minimum data set unit. The step is used to sample the data set and create the KDE.
* **precision** is used to refine the density plot at the extremities, and in the thin spots, the smallest this parameter is the more points you get on the extremities and the thin spots on the chart.
* **densityWidth** is used to widen the density. This parameter should be equal to 1 to reflect the result of the KDE values. Nevertheless, for visibility purposes, you are free to change the densityWidth to get a wider and visible shape. 
* **arg**s is one or many arrays that represent the data set. In our case, args is four arrays of weight athletes, one array for each discipline.

The function `processDensity()` returns a set of three arrays:
* **xiData** is the xAxis data generated using the step and the range of the athletes’ weights data.
* **results** includes all the density charts data.
* **stat** is the array with all the descriptive statistical coefficients.  

## Example
Check [codePen demo](https://codepen.io/mushigh/pen/eYJXjVe)

```
//Process density data
    let step = 1,
      precision = 0.00000000001,
      width = 15;

    let data = processDensity(
      step,
      precision,
      width,
      dataArray[0], //triathlon,
      dataArray[1], //badminton,
      dataArray[2] //fencing,
    );
Highcharts.chart("container", {
...
series: [
        {
          name: "Density 1",
          data: dataArray[0]
        },
        {
          name: "Density 2",
          data: dataArray[1]
        },
        {
          name: "Density 3",
          data: dataArray[2]
        }
      ]
});
```

## Remark
The function is built around the [kernel density estimation (KDE)](https://www.highcharts.com/blog/tutorials/data-science-and-highcharts-kernel-density-estimation/).
