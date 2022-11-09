# Flame graph cheat sheet
A cheat sheet for working with flame graphs.

## Debugging using flamegraphs

### Wide and tall areas are consuming most CPU.

The bar that spans the entire bottom of the graph is the function that was on-CPU (the (root) function). Hover over a function to see the function name, and click on it to see the function and its children’s information appear to the right of the graph. As the flame graph capitalizes on the hierarchical nature of function calls, parent functions are lower on the y-axis (closer to (root)), with nested functions appearing higher on the y-axis.

The width of each function on the graph represents the amount of time it took each function to execute as a percentage of the total time of the trace ((root) takes up the full width of the graph).

Some of the function columns are squat, others tall and needle-thin. The dramatic spikes are illuminating with respect to function complexity, but if they are not very wide they are being processed by the CPU quickly and are thus unlikely be the source of a CPU performance problem.

Of particular interest for flame graph analysis are functions that are both deeply-nested (high on the y-axis) and time-intensive (wide on the x-axis); such a flame graph profile is the strongest indicator that a function is improperly using CPU resources and can benefit from optimization.

## IO is not captured on a flame graph.

Typically time waiting for IO is not captured in a flamegraph since the CPU doesn't spend cycles waiting for a network call. To identify if we are waiting for IO in a flamegraoh, look at the tip of the needles to see if that is waiting on an IO function.


## Useful links
* [Miha Rekar - What Are Flame Graphs and How to Read Them, RubyConfBY 2017](https://www.youtube.com/watch?v=6uKZXIwd6M0) - Great talk in reading a flame graph.
* [CPU Flame Graphs](https://www.brendangregg.com/FlameGraphs/cpuflamegraphs.html)
