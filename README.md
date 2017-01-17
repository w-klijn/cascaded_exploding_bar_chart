# cascaded_exploding_bar_chart
Create a cascade of two or more exploding bar-charts from data with controllable typesetting.

![See graphic below for an rough example](/example.jpg?raw=true "") 

## Features
1. Size of bars in, and the total number of bar-charts is generated from data
2. Hight of bars based on raw data, normalized or percentage (each bar normalized individually)
3. Show multiple labeled relationships between stacks
4. Explosion lines to show relation between stacked bars
5. The explosion wedge can have labels and a shaded background
6. Stacked bars and boxes can have labels
7. Box labels will not display when text is to big for box (controllable)
8. Only matplotlib needed
9. Most textual and graphical elements can be typeset without changing the code
    
## Usage
Call cascaded_exploding_barcharts() with your data. If you want to typeset you
have to do this before the call.

## Input arguments cascaded_exploding_barcharts

    ax:     Axes object to plot the figure on (allows embedding in more complex 
            figures)

    data:   The input data, 3d array: A list of bar-chart data
            where each bar-chart is a list of triplets containing:
            [value, label, #color]
            See run_example() for detailed example of data structure

    emphasis: The entries in the bar-chart to emphasize and explode from and TO
            It is a 3d array: A list of triples, setting the range and the label
            The first range gives the emphasis in the source bar stack
            The second range gives the target for the explosion lines (starting
            from the emphasized range)
            e.g. To create the explosion lines in the graphical example you
            would use range: [[1,2,"EL"],[1,2,"EL"]] 
            Use None for a tripled pair not wanting emphasis 

    bar_labels: An optional label to be printed above each stack bar-chart
            (BL in the graphical example)

    representation: string
            "None": display data without normalizing (could results in 
                    different hight bars!)
            "normalized": normalize bar hight
            "percentage": normalize and multiply with 100 for %
            
            This settings has influence on the y-axis labels and how the 
            label printing is controlled. Also offset might needs to be adapted

## Typesetting

Typesetting is controlled by changing the variables in the global variable
 'exp_barch_tp_set' (A global,I know, I know).
Default typesetting is for the default matplotlib figure size and of a simple nature
changing the typesetting should be done before calling cascaded_exploding_barcharts()

    Control features (True/False):
        box_label: Print the labels in the boxes 
        bar_label: Print a label above each stack
        explode_label: Print labels between the explode lines
        explode_bg: Give the wedge between the explosion lines a color

    box_size_text_cutoff: Controls the automatic check if text is to big for a
        box (Default looks ok for standard matplotlib figure size).

The other options are either text offsets -or-
dictionaries forwarded to either axes.bar axes.line or axes.text functions 
(see matplotlib documentation for more information). 

The "zorder" is used to correctly stack the different graphical elements. It
is not advisable to change these settings.

It is possible to use named color names instead of the #rgb used currently for 
typesettings EXCEPT the bar color. The gradient method for the border
is simplistic (borderline buggy / broken) and will fail for non #rgb entries.

## Graphical example
```              
               BL           BL
            _________     _________ 
            | 3     |     | 3     |   
            |=======|_ _ _|=======|  
            | 2     |...EL|=2=====| 
            |       |.....|=1=====|
            |       |EL../| 0     |
            |=======|.../ |       |
            | 1     |../  |       |
            |       |./   |       |
            |=======|/    |       |
            | 0     |     |       |
            |_______|     |_______|
```

## TODOS
1. bar_labels must always be supplied even when turned off (can be None)
2. Major loop contains an ugly minus 1
3. Do something with the global typesetting dict exp_barch_tp_set
4. Test all corner cases of None types in emphasis
5. Check if raw plotting wedges are correct
6. It is possible to use a 'darkened' color for the box border. Lighting
   should also be possible, but rgb is hard
   
Keywords: python matplotlib exploding exploded barchart barcharts bar-chart bar-charts cascaded cascading 
