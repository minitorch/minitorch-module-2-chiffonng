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

## Notes

### Tensors [tensor_data.py](minitorch/tensor_data.py)

- Tensors are arrays of different shapes and sizes, but behind the scenes, they are all stored as a single-dimensional contiguous block of memory (aka tensor's storage)
- Tensor strides are used to index into the storage to access the elements of the tensor

### Broadcasting

- Broadcasting is a technique used to perform operations on tensors of different shapes. It involves expanding the dimensions of the smaller tensor to match the dimensions of the larger tensor

### Operations [tensor_ops.py](minitorch/tensor_ops.py)

-

### Functions

### Autograd
