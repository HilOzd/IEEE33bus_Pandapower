# Notes on Pandapower Fundamental Commands

> The dot (.) enables you to reach subelements of an object.

> In a Jupyter notebook, to learn which attributes a command has, the question mark can be used.
```python
import pandapower as pp
import pandapower.networks as nw
net = nw.mv_oberrhein()
net?
net.res_bus?
```

## Commands

*Note: Explanations of commands are given based on the bus component of the network.*

- Information about inputs and outputs of the power flow
    
    ```python
    print(net.bus)   # Gives the input data of the bus in the net
    print(net.res_bus)   # Gives the result of the bus in the net after power flow execution
    print(net)   # Shows every input/output name that you can call.
    ```

- Calling the maximum/minimum or a specific element of the variable

    ```python
    highest_vm_pu = net.res_bus.vm_pu.max()   # Gives the maximum value of the vm_pu element of the res_bus object.
    net.res_bus.vm_pu.loc[net.res_bus.vm_pu > 1.02]   # Gives only vm_pu values of the buses whose vm_pu values are 
                                                      # greater than 1.02.
    net.res_bus.loc[net.res_bus.vm_pu > 1.02]   # Gives all results of the buses whose vm_pu values are greater than 
                                                # 1.02.
    ```

    ```
    .loc[] : Access a group of rows and columns by label(s) or a boolean array.
    ```

- Plotting

    The libraries required for plotting are as follows:

    > ```python
    > from pandapower.plotting import simple_plot, simple_plotly, pf_res_plotly
    >```
    
  ```python
    simple_plot(net)   # Plots the network model, but the plot is not interactive.
    simple_plotly(net)   # Gives an interactive plot of the network model.
    pf_res_plotly(net)   # Plots the result of the power.
    bc = plot.create_bus_collection(net, buses=net.bus.index, color=colors[0], size=80, zorder=1)   # Creates the bus 
                                                                                                    # collection.
    lc = plot.create_line_collection(net, lines=net.line.index, color='grey', zorder=2)   # Creates the line collection
    ```

  - **To select specific points:**
  
    ```python
    lline_index = net.line.loc[net.line.length_km > 2.0].index   # Selects the lines longer than 2 km.
    lline = plot.create_line_collection(net, lines=lline_index, color='red', zorder=2)   # Plots specific lines in 
                                                                                         # another colour to highlight.
    ```