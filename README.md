[![Latest release](https://img.shields.io/github/release/fakenmc/generateData.svg)](https://github.com/fakenmc/generateData/releases)
[![MIT Licence](https://img.shields.io/badge/license-MIT-yellowgreen.svg)](https://opensource.org/licenses/MIT/)

# generateData

## Summary

A MATLAB/Octave function which generates 2D data clusters. Data is
created along straight lines, which can be more or less parallel
depending on the selected input parameters.

## Synopsis

```MATLAB
[data, clustPoints, idx, centers, slopes, lengths] = ...
    generateData(slope, slopeStd, numClusts, xClustAvgSep, yClustAvgSep, ...
                 lengthMean, lengthStd, lateralStd, totalPoints)
```

## Input parameters

  Parameter      | Description
  -------------- | ------------------------------------------------------------------------------------------------------
  `slopeMean`    | Mean slope of the lines on which clusters are based. Line slopes are drawn from the normal distribution.
  `slopeStd`     | Standard deviation of line slopes.
  `numClusts`    | Number of clusters (and therefore of lines) to generate.
  `xClustAvgSep` | Average separation of line centers along the X axis.
  `yClustAvgSep` | Average separation of line centers along the Y axis.
  `lengthMean`   | Mean length of the lines on which clusters are based. Line lengths are drawn from the folded normal distribution.
  `lengthStd`    | Standard deviation of line lengths.
  `lateralStd`   | Cluster "fatness", i.e., the standard deviation of the distance from each point to the respective line, in both *x* and *y* directions. This distance is obtained from the normal distribution with zero mean.
  `totalPoints`  | Total points in generated data. These will be randomly divided between clusters using the half-normal distribution with unit standard deviation.

## Return values

  Value         | Description
  ------------- | --------------------------------------------------------------------------------------
  `data`        | Matrix (`totalPoints` x *2*) with the generated data.
  `clustPoints` | Vector (`numClusts` x *1*) containing number of points in each cluster.
  `idx`         | Vector (`totalPoints` x *1*) containing the cluster indices of each point.
  `centers`     | Matrix (`numClusts` x *2*) containing line centers from where clusters were generated.
  `slopes`      | Vector (`numClusts` x *1*) containing the effective slopes of the lines used to generate clusters.
  `lengths`     | Vector (`numClusts` x *1*) containing the effective lengths of the lines used to generate clusters.

## Usage example

```MATLAB
[data cp idx] = generateData(1, 0.5, 5, 15, 15, 5, 1, 2, 200);
```

The previous command creates 5 clusters with a total of 200 points, with
a mean slope of 1 (*std*=0.5), separated in average by 15 units in both
*x* and *y* directions, with mean length of 5 units (*std*=1) and a
"fatness" or spread of 2 units.

The following command plots the generated clusters:

```MATLAB
scatter(data(:, 1), data(:, 2), 8, idx);
```

To make cluster generation reproducible, set the random number generator seed
to a specific value (e.g. 123) before generating the data:

```MATLAB
rng(123);
```

For GNU Octave, use the following instructions instead:

```MATLAB
rand("state", 123);
randn("state", 123);
```

## Reference

If you use this function in your work, please cite the following reference:

- Fachada, N., Figueiredo, M.A.T., Lopes, V.V., Martins, R.C., Rosa,
A.C., [Spectrometric differentiation of yeast strains using minimum volume
increase and minimum direction change clustering criteria](http://www.sciencedirect.com/science/article/pii/S0167865514000889),
Pattern Recognition Letters, vol. 45, pp. 55-61 (2014), doi: http://dx.doi.org/10.1016/j.patrec.2014.03.008

## License

This script is made available under the [MIT License](LICENSE).
