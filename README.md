# SuperWeight-Moondream

Paper implementation for [The Super Weight in Large Language Models](https://arxiv.org/abs/2411.07191)

Wanted to check if super weights exist for Moondream as well. Curious because I belive Vik was doing Quantization aware training and pruning. Should be a fun experiment.

Note: Code and weights are from the official `revision="2025-04-14"`

### Notes:

#### Super Activations a.k.a large activation spikes
* persist across layers
* have constant magnitude
* exist at same position irrespective of input
* activation's channel aligns with the super weight's channel
* activation first appears right after our super weight

Locating super weights by using activation spikes:
* Detect spikes in mlp.down_proj inputs and outputs across layers
* Prune the super weight, check the magnitude of the activation, if its drastically reduced, its a super weight.
* Repeat the same for all the activation spikes that remain after removing each super weight. So far the most seuper weights discovered was for Phi-3-instruct in the paper i.e 6. I think Moondream might behave similarly to Phi-3.

The models in the paper are all Decoder models. None of them have a Vision Encoder. I'll also take a look at the vision encoder mlp later but lets look at the decoder for now.

## Other research

1. Check the branch: fewshot for one/few shot prompting for moondream. Colab [here](https://colab.research.google.com/drive/1cQLDghIMUN5lckITpMU4iWGVtO5n478M?usp=sharing)
