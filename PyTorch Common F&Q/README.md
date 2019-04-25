1. `register_hook()`与`register_backward_hook()`以及`register_forward_hook()`有什么区别和联系吗？
   > The former is applied to a tensor variable, while the latter two are applied to a layer module.

2. `tensor.detach()`是用来做什么的？
   > It creates a tensor that shares storage with tensor that does not require grad. 

   > [Pytorch Forum](https://discuss.pytorch.org/t/clone-and-detach-in-v0-4-0/16861/2)

3. `tensor.clone()`是用来做什么的？
   > It creates a copy of tensor that imitates the original tensor's `requires_grad` field. 

   > You should use `detach()` when attempting to remove a tensor from a computation graph, and use `clone()` as a way to copy the tensor while still keeping the copy as a part of the computation graph it came from.

