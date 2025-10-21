Create a .NET 8 C# console project with a stub Main method. (Specification only—do not include implementation code in this file.)

Functionality:
- Generate a set of data points (x, f(x)) where f(x) is a non-linear function with excessive random noise.
- Plot the generated data points using a scatter plot.

Follow these steps to implement the required functionality:

1)
Add required NuGet packages:
- ScottPlot (recommended for console plotting): dotnet add package ScottPlot
- MathNet.Numerics (optional for advanced math): dotnet add package MathNet.Numerics

2)
Add required using directives in Program.cs :
using System;
using System.Collections.Generic;
using System.Linq;
using ScottPlot;
using MathNet.Numerics;

3)
Create a static method 'GenData' that generates a set of data points (x, f(x)) and returns them as a List of objects or a DataTable.
Arguments:
- 'xRange' is a tuple (ValueTuple) of two integers representing the range of x values to generate.
Returns:
- A List or DataTable with two columns, 'x' and 'y'.
Details:
- 'x' values are generated randomly between xRange.Item1 and xRange.Item2.
- 'y' values are generated as a non-linear function of x with excessive random noise: y = Math.Pow(x, 1.5) + noise.
- The result is sorted by the 'x' values.
Error Handling:
- If xRange is not a tuple of two integers, throw an ArgumentException.
- If xRange.Item1 is not less than xRange.Item2, throw an ArgumentException.
Example usage (illustrative only, not implemented here):
var data = GenData((0, 100));

4)
Create a static method 'PlotData' that plots the data points from the List or DataTable. The Copilot response should contain XML doc comments for the method.
Arguments:
- 'data' is a List or DataTable with two columns, 'x' and 'y'.
Returns:
- void
Details:
- The data points are plotted as a scatter plot using ScottPlot or OxyPlot.
- The plot has a title 'Data Points', x-axis label 'x', and y-axis label 'f(x)'.
Error Handling:
- If 'data' is not a List or DataTable with two columns, throw an ArgumentException.
Example usage (illustrative only, not implemented here):
var data = GenData((0, 100));
PlotData(data);

5)
Modify the 'Main' method to call 'GenData' and 'PlotData' to generate and plot the data points.

6)
Execute the app.


