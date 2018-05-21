# Contributing

**Are you new to open source and GitHub?**
If so, reading the "[How to submit a contribution](
https://opensource.guide/how-to-contribute/#how-to-submit-a-contribution)"
guide will provide a great introduction to contributing to MODELFIT and other
Open Source projects.
All the MODELFIT-specific contributing instructions listed below will make much
more sense after reading this guide.

If you are new to the project don't forget to add your name and affiliation to
the `.zenodo.json` file.

## Code style guide

### Function and variable names

Whenever possible, instances of Nodes and Workflows should use the same names
as the variables they are assigned to.
This makes it easier to relate the content of the working directory to the code
that generated it when debugging.

Workflow variables should end in `_wf` to indicate that they refer to Workflows
and not Nodes.
For instance, a workflow whose basename is `myworkflow` might be defined as
follows:

```Python
from nipype.pipeline import engine as pe

myworkflow_wf = pe.Workflow(name='myworkflow_wf')
```

If a workflow is generated by a function, the name of the function should take
the form `init_<basename>_wf`:

```Python
def init_myworkflow_wf(name='myworkflow_wf):
    workflow = pe.Workflow(name=name)
    ...
    return workflow

myworkflow_wf = init_workflow_wf(name='myworkflow_wf')
```

If multiple instances of the same workflow might be instantiated in the same
namespace, the workflow names and variables should include either a numeric
identifier or a one-word description, such as:

```Python
myworkflow0_wf = init_workflow_wf(name='myworkflow0_wf')
myworkflow1_wf = init_workflow_wf(name='myworkflow1_wf')

# or

myworkflow_lh_wf = init_workflow_wf(name='myworkflow_lh_wf')
myworkflow_rh_wf = init_workflow_wf(name='myworkflow_rh_wf')
```