# I/O Description of the TotalEnergyWC:

Short documentation of the input and output nodes of a TotalEnergyWC

## Inputs:

### Common:

1. StructureData, structure: The crystal structure
2. ParameterData, options: contains a dictionary with all usable options from AiiDA.

### Code Specific input types:

1. Code node(s), or as string?
2. Calculation specific ParameterData
3. (workflow specific ParameterData)


## Outputs:

### Common:

1. ParameterData, output_parameters: Contains a dictionary containingi at least: {‘energy’ : value, ‘energy_units’ : ‘eV’}
2. TrajectoryData, forces: Contains the forces for each atom in the structure and the crystal structure. Forces are in eV per Angstrom.



