# Implementation Guide: Interactive Electrical Fault Simulator

## Overview

This guide provides instructions for implementing the Interactive Electrical Fault Simulator for Power Systems Education. The simulator visualizes fault current flows in a 33kV electrical distribution network, helping students and engineers understand complex fault scenarios through clear, animated visualizations.

## Technical Requirements

- Modern web browser (Chrome, Firefox, Safari, or Edge)
- No additional libraries required - the implementation is self-contained
- Basic web server to host the HTML file (optional for local use)

## Implementation Steps

### 1. Setting Up the Project

1. Create a new directory for the project
2. Save the provided HTML code as `index.html` in this directory
3. No additional files are needed - all CSS and JavaScript is embedded in the HTML file

### 2. Testing Locally

1. Open the `index.html` file directly in a web browser for local testing
2. Alternatively, set up a basic web server to serve the file:
   - Python: `python -m http.server` (in the project directory)
   - Node.js: Use tools like `http-server` or `live-server`

### 3. Customizing the Simulator

The simulator is designed to be self-contained and customizable. Here are some common customizations:

#### Modifying System Parameters

In the JavaScript section, you can adjust default values for:

```javascript
// Power system parameters
const powerSystemParams = {
    systemVoltage: 33, // kV
    sourceMVA: 500, // MVA
    frequency: 50, // Hz
    // ...
};
```

#### Adjusting Visual Styling

The CSS variables at the top of the file control the color scheme:

```css
:root {
    --primary-color: #2c3e50;
    --secondary-color: #0d6efd;
    --warning-color: #ffc107;
    --danger-color: #dc3545;
    /* ... */
}
```

#### Adding Additional Fault Types

To add new fault types:

1. Add new radio button options in the HTML
2. Extend the fault calculation logic in `calculateFaultCurrents()`
3. Update the current flow visualization in `updateCurrentFlows()`

#### Modifying Network Topology

To change the network topology:

1. Adjust the `drawNetworkDiagram()` function to include new components
2. Update coordinates and connections as needed
3. Add any new current flow paths in `updateCurrentFlows()`

## Core Functions Explanation

### Fault Current Calculations

The `calculateFaultCurrents()` function implements simplified fault calculations based on IEC 60909 standards:

1. **Initial Symmetrical Current (Ik")**: Calculated using system voltage, impedance, and voltage factor
2. **Peak Current (Ip)**: Calculated using the kappa factor based on X/R ratio
3. **Steady-State Current (Ik)**: Simplified as 80% of the initial current
4. **DC Component**: Calculated based on point-on-wave and X/R ratio, affecting the peak current magnitude

The fault current calculations are adjusted based on fault type:
- Three-phase fault (L-L-L): Uses full calculated values
- Phase-to-phase fault (L-L): Applies a multiplier of √3/2 to the three-phase fault current
- Single-phase-to-earth fault (L-G): Applies a multiplier of √3/3, with adjustments for earth return
- Phase-to-phase-to-earth fault (L-L-G): Applies a multiplier of √3/√2, with adjustments for earth return

### Waveform Visualization

The `drawWaveforms()` function creates time-domain visualizations of the fault currents:

1. Sets up the canvas coordinate system with appropriate scaling
2. Calculates the maximum current to establish Y-axis scaling
3. For each phase involved in the fault:
   - Calculates instantaneous current values using the formula: i(t) = √2 * Irms * sin(ωt + phase) + Idc * e^(-t/τ)
   - Draws the waveform using HTML Canvas
   - Identifies and marks the peak current value
4. Adds the DC offset component as a separate dashed line
5. Includes axis labels, legends, and other visual elements

### Network Diagram and Current Flow Animation

The network visualization uses SVG elements to create an interactive diagram:

1. `drawNetworkDiagram()` creates the basic network topology:
   - Power source/grid representation
   - Transformer with neutral earthing connection
   - 33kV busbar
   - Circuit breaker
   - Outgoing feeders with three-phase representation

2. `updateCurrentFlows()` adds animated current paths based on fault type:
   - Identifies which phases are involved in the fault
   - Creates animated lines using CSS animations (`stroke-dasharray` and `animation`)
   - Adds earth return paths for ground faults
   - Visually distinguishes different phases with color coding

3. Circuit breaker animation is handled by toggling CSS classes that control the visual state

## Educational Content Integration

The simulator incorporates educational content in several ways:

1. **Tab-based Information**: The interface includes tabs for "Current Waveforms," "Current Parameters," and "Educational Notes"

2. **Parameter Displays**: Real-time calculation results show key fault current values (Ik", Ip, Ik)

3. **Interactive Info Panel**: Context-specific information appears when clicking the "Educational Information" button

4. **Tooltips and Labels**: Components are clearly labeled for easy identification

## Troubleshooting and Extensions

### Common Issues

1. **Canvas Not Rendering**: If the waveform canvas appears blank:
   - Check browser console for errors
   - Verify the canvas has proper dimensions (the `resizeCanvas()` function should handle this)
   - Ensure fault parameters are within reasonable ranges

2. **Animation Issues**: If current flow animations aren't working:
   - Verify CSS animations are supported in your browser
   - Check that SVG elements are properly created with correct class names
   - Inspect the network diagram paths to ensure they're properly positioned

3. **Calculation Anomalies**: If fault current values seem incorrect:
   - Verify input parameters (system voltage, source MVA, X/R ratio)
   - Check fault type selection and corresponding calculations
   - Compare results with manual calculations using IEC 60909 formulas

### Potential Extensions

1. **Advanced Fault Types**: 
   - Implement evolving faults (e.g., L-G developing into L-L-G)
   - Add high-impedance fault models
   - Include cross-country fault scenarios

2. **Protection Coordination**:
   - Add protection relay visualization
   - Implement time-current characteristic curves
   - Visualize protection coordination between devices

3. **System Expansion**:
   - Extend to multi-feeder systems
   - Add distributed generation sources
   - Implement more complex network topologies

4. **Data Export**:
   - Add capability to export simulation results
   - Generate reports with fault calculations
   - Create printable educational materials

## Standards Compliance

The simulator calculations are based on:

1. **IEC 60909**: "Short-circuit currents in three-phase AC systems"
   - Uses voltage factor c for maximum short-circuit calculations
   - Implements kappa factor for peak current calculation
   - Accounts for X/R ratio effects on DC component

2. **ENA EREC G74**: "Procedure to meet the requirements of IEC 60909"
   - Follows industry-standard approach for fault calculations
   - Uses appropriate multipliers for different fault types
   - Considers system earthing in fault current paths

## Conclusion

This interactive electrical fault simulator provides a valuable educational tool for understanding power system fault behavior. The implementation combines accurate calculations based on industry standards with clear visualizations to make complex concepts more accessible.

By following this guide, you can successfully implement, customize, and extend the simulator for various educational and practical applications in electrical power systems education.

## References

1. IEC 60909-0:2016 - Short-circuit currents in three-phase AC systems
2. ENA EREC G74 - Procedure to meet the requirements of IEC 60909
3. J. Schlabbach, "Short-circuit Currents," IET Power and Energy Series
4. A.T. Johns, S.K. Salman, "Digital Protection for Power Systems," IET Power and Energy Series