
# deep vector quantization

Random experiments with VQVAE and friends, i.e. autoencoder models that pass through discrete latent variable bottlenecks, which are then easy to subsequently plug into existing infrastructure for modeling sequences of discrete variables (GPT and friends). I didn't get a chance to make the code pretty and consume and propagate all the proper args etc. - currently this is very much not a "pass arguments in watch it work" kind of repo, this is "read the entire code and hack things inline" code.

DeepMind's [VQVAE](https://github.com/deepmind/sonnet/blob/v2/examples/vqvae_example.ipynb)

Should train out of the box as `python train_vqvae.py --gpus 1 --vq_flavor vqvae`.

I am able to get what I think are expected results on CIFAR-10 using VQVAE (judging by reconstruction loss achieved). However I had to resort to a data-driven intialization scheme with k-means, which the sonnet repo does not use, potentially due to more careful model initialization treatment. When I do not use data-driven init the training exhibits catastrophic index collapse.

Jang et al. [Gumbel Softmax](https://arxiv.org/abs/1611.01144) version, also the version used in [DALL-E](https://openai.com/blog/dall-e/) allegedly, though we have not seen the details yet.

Should train out of the box as `python train_vqvae.py --gpus 1 --vq_flavor gumbel`.

Trains and converges to slightly higher reconstruction loss, but tuning the scale of the kl divergence loss and the temperature decay rate and the version of gumbel (soft/hard) has so far proved a little bit finicky. Also the whole thing trains much slower. Requires a bit more thorough hyperparameter search than a few one-off guesses.
