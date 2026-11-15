# unisic-models

Model files that [Unisic](https://github.com/unisic/unisic) downloads on request, published as release assets. Nothing here is code; the app pins each file by URL, size and SHA-256 (`kPins` in `src/editor/BackgroundRemover.cpp`) and refuses anything else.

They live in their own repository because Unisic's beta update channel reads the newest release of `unisic/unisic`, so a model release there would hide the next app release from beta users.

## birefnet-lite-dcn-1

`birefnet-lite-dcn.onnx`, 181120537 bytes, SHA-256 `ef0bfeb72e5d83fa032433b4017accd338b74bcfb98af53f3240a751ef0ae961`. Used by "Remove background" in the editor.

[BiRefNet](https://github.com/ZhengPeng7/BiRefNet) lite (MIT, see `LICENSE`), from the [onnx-community export](https://huggingface.co/onnx-community/BiRefNet_lite-ONNX) at commit `de15b22`, with each of its 20 expanded deformable convolutions replaced by one ONNX `DeformConv` (opset 19). Same weights; it needs ONNX Runtime 1.25 or newer. Rebuild and check it byte for byte with [`scripts/birefnet-deformconv.py`](https://github.com/unisic/unisic/blob/dev/scripts/birefnet-deformconv.py) in the Unisic repository.

## ppocr-v6-1

Used by the "Better OCR model" (Linux). Two sizes, each a detection and a recognition model; Unisic downloads one size, on request.

| File | Bytes | SHA-256 |
| --- | --- | --- |
| `PP-OCRv6_det_tiny.onnx` | 1829618 | `f42c0fbd294d95eac1a550e131b277dac97462c8025fa4b6c3cec1b7894bd3d5` |
| `PP-OCRv6_rec_tiny.onnx` | 4489813 | `e16e242de5937ad92609223f19bc2aff3727ee40b095f996907c24749bad251b` |
| `PP-OCRv6_det_small.onnx` | 9929594 | `090f04abcd9d9a7498bc4ebf677e4cb9bdce1fe4197ddb7e529f1ef44e1ff94f` |
| `PP-OCRv6_rec_small.onnx` | 21234383 | `6f327246b50388f3c176ae304bd95767ea6dc0c9ae92153ef8cbe210b3c14884` |

PP-OCRv6 by [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) (Apache-2.0, see `LICENSE-PaddleOCR.txt` in the release), as [RapidOCR](https://github.com/RapidAI/RapidOCR) 3.10 exports it to ONNX: byte for byte the files its `default_models.yaml` pins. The recognition dictionary is embedded in each recognition model (ONNX metadata key `character`). No angle classifier is used.
