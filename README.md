# Interactive Electrical Fault Simulator

## Overview

The Interactive Electrical Fault Simulator is an educational web application designed to help electrical engineering students, power systems engineers, and technical educators understand complex fault scenarios in a 33kV electrical distribution network. Through clear, animated visualizations, users can explore different fault types, observe current flows, and learn about circuit breaker behavior.

![Simulator Screenshot](screenshot.png)

## Features

- **Interactive Network Visualization**
  - Professional electrical diagram with industry-standard symbols
  - Clear representation of power grid, transformer, busbar, circuit breaker, and feeders
  - Visible neutral earthing connection
  - Color-coded phase identification

- **Comprehensive Fault Simulation**
  - Five operational modes:
    - Normal operation (no fault)
    - Three-phase fault (L-L-L)
    - Phase-to-phase fault (L-L)
    - Single-phase-to-earth fault (L-G)
    - Phase-to-phase-to-earth fault (L-L-G)
  - Animated current flows showing distinct paths for each phase
  - Earth return path visualization for ground faults
  - Interactive circuit breaker control

- **Educational Content**
  - Real-time waveform visualization with AC and DC components
  - Current parameter calculations (Ik", Ip, Ik)
  - Context-sensitive educational information
  - Standards-compliant calculations (IEC 60909, ENA EREC G74)

- **Customizable Parameters**
  - Point-on-wave fault initiation
  - X/R ratio adjustment
  - Fault resistance control
  - System voltage and source MVA settings

## Technical Requirements

- Modern web browser (Chrome, Firefox, Safari, or Edge)
- No additional libraries required - the implementation is self-contained
- Basic web server to host the HTML file (optional for local use)

## Installation

1. Clone or download this repository
2. Open `index.html` in a web browser

For server deployment:
```bash
# Using Python's built-in HTTP server
python -m http.server

# Or with Node.js
npx http-server
```

## Usage Guide

### Basic Operation

1. **Select Fault Type**: Choose from the available fault types using the radio buttons
2. **Choose Fault Location**: Select where the fault occurs in the network
3. **Adjust Parameters**: Modify the point-on-wave, X/R ratio, and other parameters as needed
4. **Run Simulation**: Click the "Run Simulation" button to see the results
5. **Toggle Circuit Breaker**: Use the button to open/close the circuit breaker and observe effects

### Understanding the Visualization

- **Network Diagram**: Shows the power system components and animated current flows
- **Waveform Display**: Visualizes the current waveforms for each phase
- **Parameter Tab**: Displays calculated fault current values
- **Educational Notes**: Provides explanation of fault types and current parameters

## Customization

The simulator is designed to be easily customizable:

- Modify CSS variables to change the color scheme
- Adjust default power system parameters in the JavaScript code
- Extend the network topology by modifying the SVG generation functions

## Educational Context

This simulator helps users understand:

- Different types of electrical faults and their characteristics
- How fault currents are calculated and what they mean
- The role of X/R ratio and point-on-wave in fault behavior
- Circuit breaker operation and phase interruption
- The significance of peak current (Ip) in equipment selection

## Standards Compliance

The simulator's calculations are based on:

- IEC 60909: "Short-circuit currents in three-phase AC systems"
- ENA EREC G74: "Procedure to meet the requirements of IEC 60909"

## Troubleshooting

- **Blank Waveform**: Ensure your browser supports HTML Canvas and JavaScript is enabled
- **No Animations**: Check that your browser supports CSS animations
- **Calculation Issues**: Verify input parameters are within reasonable ranges

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is released under the MIT License. See the LICENSE file for details.

## Acknowledgments

- Developed as an educational tool for power systems engineering
- Inspired by industry-standard fault calculation methods
- Created to make complex electrical concepts more accessible through visual learning
