# Plantaloon plant scanner model

The on-phone plant recognition model used by **Plantaloon**, a free, private, open-source
houseplant care app for Android. The app downloads this file once, when you first use
"Scan a plant"; photos are matched on the phone and never uploaded.

## The file

`bioclip_image_int8.onnx` (release `v1`) is the **image encoder of
[BioCLIP](https://huggingface.co/imageomics/bioclip)** (ViT-B/16), unchanged apart from being
exported to ONNX and quantized to 8-bit integers (dynamic quantization) so it runs on phones.

- Input: `image`, float32 `[1, 3, 224, 224]`, RGB, resized so the short side is 224 px,
  centre-cropped, normalised with mean `[0.48145466, 0.4578275, 0.40821073]` and
  std `[0.26862954, 0.26130258, 0.27577711]`.
- Output: `embedding`, float32 `[1, 512]`, L2-normalised.
- SHA-256: see the release notes.

The app compares the embedding with fingerprints of the plants in its catalog (species names
plus openly licensed example photos from iNaturalist contributors). Those fingerprints ship
inside the app, not here.

## Credit and licence

BioCLIP is by Samuel Stevens, Jiaman Wu, Matthew J. Thompson, Elizabeth G. Campolongo,
Chan Hee Song, David Edward Carlyn, Li Dong, Wasila M. Dahdul, Charles Stewart,
Tanya Berger-Wolf, Wei-Lun Chao and Yu Su (Imageomics Institute), fine-tuned from OpenAI's CLIP,
and is released under the MIT licence, reproduced in [LICENSE](LICENSE). This converted file is
distributed under the same licence. Please cite BioCLIP if you use it:

> Stevens et al., *BioCLIP: A Vision Foundation Model for the Tree of Life*, CVPR 2024.
> https://doi.org/10.48550/arXiv.2311.18803
