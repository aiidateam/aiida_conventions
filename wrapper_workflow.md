# Wrapper workflow definition

We define here as "wrapper workflow" the actual workflow that a user will call to run a given task, independent of the code to use.
The main task of this workflow is to "redirect" all inputs to the specific implementation (here we use as an example `TotalEnergyWorkchain` as an example).

## Workflow inputs and outputs
- This workflow will just expose the same inputs of any workflow, but add a new one, a `Str` Data node, with linkname `worfklow_entrypoint`.

- The content is the entrypoint string of a workflow to load. The workflow will:
  - load this workflow
  - forward all inputs
  - collect the outputs at the end and return the output data as defined by `TotalEnergyWorkchain`.

So the outputs at this stage will be the same as `TotalEnergyWorkchain` (to decide if we need additional "log" output).

## Utility functions
In order to allow to create a GUI automatically by inspecting the workflow, we will provide utility functions to get automatically information on the possible parameters.

We start with the code (or codes) to pass as input, and over time we see if/how this can be extended to other parameters.

### get_valid_entrypoints
- `def get_valid_entrypoints()`: this function will return a list of valid entrypoints installed in the current virtual environment (by looping over the installed plugins); any of these values will be acceptable as input for the workchain with input `workflow_entrypoint`.

  - this can be generalized not to return only a string, but a dictionary, e.g.:
    ```json
    {
         "entry_point": "xxx",
         "description": "yyy"
    }
    ```

  - note: this might require to keep an internal "registry" of known `TotalEnergyWorkchain` workflow implementations.

- `def get_code_input_link_labels(entrypoint)`: this function returns a list of all required link labels for input codes. Often, this function will return only `['code']` if only one code is required, with label `code`. If more codes are needed, all are listed here (e.g. `[code_prepareinput, code_run]`)
- `def get_available_codes(entrypoint, code_input_label)`: this returns a list of codes that are acceptable for the given `entrypoint` and `code_input_label`. Internally, this does a query on all codes that match, e.g. by looking at the `default_input_plugin`.

Note: Once we start implementing some of the functions above, we can either decide to store all this information in a single central repository, or we can ask each workchain to expose methods to discover what is required (already now, one could inspect the `spec` e.g. to know which inputs are codes and what are their labels; it would be good to add also info, e.g., on the expected (one or more) `default_input_plugin`).

## Example implementation
To prove the functionality, we should create a generic "Equation of State" (EOS) workchain that computes the EOS independent of the code, and probably prepare also an AiiDA Lab app to prepare the GUI (and pre-fill e.g. dropdown boxes with the codes using the utility functions described above).

