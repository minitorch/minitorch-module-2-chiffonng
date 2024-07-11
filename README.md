[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=15367888&assignment_repo_type=AssignmentRepo)

# MiniTorch Module 2

<img src="https://minitorch.github.io/minitorch.svg" width="50%">

- Docs: https://minitorch.github.io/

- Overview: https://minitorch.github.io/module2/module2/

This assignment requires the following files from the previous assignments. You can get these by running

```bash
python sync_previous_module.py previous-module-dir current-module-dir
```

The files that will be synced are:

        minitorch/operators.py minitorch/module.py minitorch/autodiff.py minitorch/scalar.py minitorch/module.py project/run_manual.py project/run_scalar.py

## TODOS

Sandbox for Math Functions on Streamlit fails to run.

## Debug

### Failed Test Case

Isolate the error in the code and run hypothesis in verbose mode to see the failing test case.

```bash
HYPOTHESIS_VERBOSITY_LEVEL=verbose pytest -v -s tests/test_tensor.py::test_permute
```

### minitorch not found

If installing `minitorch` fails, first find the path to the `minitorch` directory.

```bash
pip show minitorch
```

Then we have three options to resolve the issue:

1.  Add the path to the `minitorch` directory to the `PYTHONPATH` environment variable. This is a permanent solution. Reload the terminal after running the command.

        ```bash
        export PYTHONPATH=$PYTHONPATH:/path/to/minitorch
        ```

2.  Temporarily add the path to the `PYTHONPATH` variable when running commands

        ```bash
        PYTHONPATH=$PYTHONPATH:/path/to/minitorch streamlit run project/app.py
        ```

3.  Add the following to the beginning of affected scripts, `graph_builder.py` and `run_tensor.py`. Then reload the Streamlit app.

        ```python
        import sys
        sys.path.append("/path/to/minitorch")
        ```

## Notes

### Tensors [tensor_data.py](minitorch/tensor_data.py)

- Tensors are arrays of different shapes and sizes, but behind the scenes, they are all stored as a single-dimensional contiguous block of memory (aka tensor's storage)
- Tensor strides are used to index into the storage to access the elements of the tensor

### Broadcasting

- Broadcasting is a technique used to perform operations on tensors of different shapes. It involves expanding the dimensions of the smaller tensor to match the dimensions of the larger tensor

### Operations [tensor_ops.py](minitorch/tensor_ops.py)

- `map` applies a function to each element of a tensor
- `zip` applies a function to pairs of elements from two tensors
- `reduce` applies a function to a tensor along a given dimension

### Autograd [tensor_functions.py](minitorch/tensor_functions.py)

Derivatives mostly scale up scalar derivatives ([scalar_functions](minitorch/scalar_functions.py)) to tensor derivatives.

Some gradients that are not readily defined:

- Sigmoid: $$\sigma'(x) = \sigma(x) \cdot (1 - \sigma(x))$$
- Permutation: This is not a differentiable operation since it doesn't change the values within the tensor, only their layout. However, during autograd, we can still compute the gradients by permuting the gradients in the backward pass.
  - Forward Pass: The tensor is permuted according to the specified order.
  - Backward Pass: The gradients are permuted back to their original order.
