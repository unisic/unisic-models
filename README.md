# unisic-models

Model files that [Unisic](https://github.com/unisic/unisic) downloads on request, published as release assets. Nothing here is code; the app pins each file by URL, size and SHA-256 (`kPins` in `src/editor/BackgroundRemover.cpp`) and refuses anything else.

They live in their own repository because Unisic's beta update channel reads the newest release of `unisic/unisic`, so a model release there would hide the next app release from beta users.

## birefnet-lite-dcn-1

`birefnet-lite-dcn.onnx`, 181120537 bytes, SHA-256 `ef0bfeb72e5d83fa032433b4017accd338b74bcfb98af53f3240a751ef0ae961`. Used by "Remove background" in the editor.

[BiRefNet](https://github.com/ZhengPeng7/BiRefNet) lite (MIT, see `LICENSE`), from the [onnx-community export](https://huggingface.co/onnx-community/BiRefNet_lite-ONNX) at commit `de15b22`, with each of its 20 expanded deformable convolutions replaced by one ONNX `DeformConv` (opset 19). Same weights; it needs ONNX Runtime 1.25 or newer. Rebuild and check it byte for byte with [`scripts/birefnet-deformconv.py`](https://github.com/unisic/unisic/blob/dev/scripts/birefnet-deformconv.py) in the Unisic repository.
