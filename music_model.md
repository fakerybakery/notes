# Music model

**Codecs**

- S1-DAC is pretty good but NC-licensed
- Then we have DAC and DACVAE

On testing DACVAE is pretty good on music - good enough but not great. It still sounds a bit artificial and reconstruction is not perfect. So it probably needs finetuning. It is already ~95% of the way there, I think it was just optimized for speech so hopefully additional training can get it the final 5% of the way there. But good enough for initial experiments.

**Architecture**

We can adapt Echo-TTS which is a DiT-based model. In Echo, Jordan trains the text encoder from scratch, this is fine for lyrics but we probably don't want it for the description input. And for a music model for now we probably don't want to do music voice cloning, just text-based prompting. So we can use a pretrained model for the tags and keep the from-scratch text encoder.

The base Echo-TTS model already supports multi-speaker speech using `[S1]`, `[S2]`, etc., so adding sections such as `[Intro]`, `[Chorus]` etc. should be feasible.

There's the question of whether to train Echo-TTS for longer sequences (>30s) or just use blockwise diffusion. Blockwise diffision is probably best to start, cheaper to train.

**Dataset**

To start, a synthetic music dataset is probably the best. Can use an existing dataset we already have such as the Suno (700k) or Udio (few million but many duplicates) datasets. Perhaps synthetic music can be used to create a base model and others can finetune it on their own data. I don't think synthetic data alone will make a very good model at all, though it is much less risky to use synthetic data.