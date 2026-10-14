# WT-ReID

Metadata for **WT-ReID**, a benchmark for pure-texture wildlife individual re-identification, assembled from six subsets of **WildlifeReID-10K**~[1].

> **No images are distributed in this repository.** The underlying imagery remains the property of its original publishing teams. This repository releases the benchmark metadata only (a single CSV file), which fully determines the WT-ReID benchmark when combined with the WildlifeReID-10K imagery.

## Benchmark at a glance

| Item | Value |
| --- | --- |
| Images | 24,436 |
| Identities | 3,142 |
| Species | 5 (tiger, leopard, hyena, zebra, giraffe) |
| Subsets | 6 (ATRW, LeopardID2022, HyenaID2022, GiraffeZebraID, StripeSpotter, Giraffes) |
| Training split | 19,015 images / 2,995 identities |
| Testing split | 5,421 images / 1,443 identities |
| Shared test identities | 1,296 (appear in both splits) |
| Unseen test identities | 147 (appear in the testing split only) |

### Per-subset statistics

| Subset | Species | Turing pattern | Identities | Train IDs | Test IDs | Unseen IDs | Images | Train | Test |
| --- | --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| ATRW | tiger | striped | 182 | 174 | 182 | 8 | 5,415 | 4,325 | 1,090 |
| LeopardID2022 | leopard | spotted | 430 | 413 | 383 | 17 | 6,806 | 5,342 | 1,464 |
| HyenaID2022 | hyena | spotted | 256 | 247 | 256 | 9 | 3,129 | 2,497 | 632 |
| GiraffeZebraID | zebra & giraffe | striped & patched | 2,051 | 1,948 | 448 | 103 | 6,898 | 5,290 | 1,608 |
| StripeSpotter | zebra | striped | 45 | 43 | 44 | 2 | 820 | 655 | 165 |
| Giraffes | giraffe | patched | 178 | 170 | 130 | 8 | 1,368 | 906 | 462 |
| **Total** | **5 species** | — | **3,142** | **2,995** | **1,443** | **147** | **24,436** | **19,015** | **5,421** |

The curation and partition protocol follows WildlifeReID-10K: image files never overlap between the training and testing splits, and unseen identities are present in every subset.

## Files

### `WT-ReID_metadata.csv`

One row per image (24,436 rows + header).

| Column | Type | Description |
| --- | --- | --- |
| `identity` | str | Global identity label. Unique within a subset, e.g. `ATRW_16`. |
| `path` | str | Relative path of the image with respect to the root directory of the extracted WildlifeReID-10K release, e.g. `images/ATRW/atrw_reid_train/train/001970_0004d0b59e19461f.jpg`. |
| `date` | str | Capture date as reported by the source dataset. Optional and sparse (empty for most subsets). |
| `orientation` | str | Viewpoint label as reported by the source dataset. Optional and sparse (empty for most subsets). |
| `species` | str | Species category: `tiger`, `leopard`, `hyena`, `zebra` or `giraffe`. |
| `split` | str | `train` or `test`, following the WildlifeReID-10K partition protocol. |
| `dataset` | str | Name of the source subset (one of the six listed above). |
| `cluster_id` | str | Optional identifier combining the identity label with an integer index, e.g. `ATRW_16_0`. Empty for some subsets. Reproduced as provided by the source annotations and **not used** by the WT-ReID evaluation protocol. |

## Reconstruction

1. Obtain the WildlifeReID-10K imagery and extract it. Call the extracted root directory `WILD` (it contains an `images/` folder).
2. Copy `WT-ReID_metadata.csv` into `WILD/`.
3. Resolve each row by joining its `path` column with `WILD`.
4. Train on rows with `split == "train"`; evaluate on rows with `split == "test"`. The testing split contains 1,296 identities shared with the training set and 147 identities that appear only in the testing split.

## Citation

If you use WT-ReID, please cite the following sources.

### WT-ReID

<!-- TODO: add the full citation of the WT-ReID paper here once available. -->

### WildlifeReID-10K

```bibtex
@inproceedings{adam2025wildlifereid10k,
  author    = {Adam, Luk{\'a}{\v{s}} and {\v{C}}erm{\'a}k, Vojt{\v{e}}ch and Papafitsoros, Kostas and Picek, Lukas},
  title     = {WildlifeReID-10k: Wildlife Re-Identification Dataset with 10k Individual Animals},
  booktitle = {2025 IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops (CVPRW)},
  pages     = {2090--2100},
  year      = {2025},
  doi       = {10.1109/CVPRW67362.2025.00197}
}
```

### Original image sources

The six subsets originate from the following datasets; please cite them as well.

```bibtex
@inproceedings{li2020atrw,
  author    = {Li, Shuyuan and Li, Jianguo and Tang, Hanlin and Qian, Rui and Lin, Weiyao},
  title     = {{ATRW}: A Benchmark for Amur Tiger Re-identification in the Wild},
  booktitle = {Proceedings of the 28th ACM International Conference on Multimedia},
  pages     = {2590--2598},
  year      = {2020},
  doi       = {10.1145/3394171.3413569}
}

@inproceedings{lahiri2011biometric,
  author    = {Lahiri, Mayank and Tantipathananandh, Chayant and Warungu, Rosemary and Rubenstein, Daniel I. and Berger-Wolf, Tanya Y.},
  title     = {Biometric animal databases from field photographs: identification of individual zebra in the wild},
  booktitle = {Proceedings of the 1st ACM International Conference on Multimedia Retrieval},
  pages     = {1--8},
  year      = {2011}
}

@misc{bpc2022leopardhyena,
  author       = {{BPCT}},
  title        = {Panthera pardus {CSV} custom export},
  year         = {2022},
  howpublished = {African Carnivore Wildbook},
  note         = {Datasets available at \url{https://lila.science/datasets/leopard-id-2022/} and \url{https://lila.science/datasets/hyena-id-2022/}}
}

@article{miele2021revisiting,
  author  = {Miele, Vincent and Dussert, Gaspard and Spataro, Bruno and Chamaill{\'e}-Jammes, Simon and Allain{\'e}, Dominique and Bonenfant, Christophe},
  title   = {Revisiting animal photo-identification using deep metric learning and network analysis},
  journal = {Methods in Ecology and Evolution},
  volume  = {12},
  number  = {5},
  pages   = {863--873},
  year    = {2021}
}

@inproceedings{parham2017aaai,
  author    = {Parham, Jason and Crall, Jonathan and Stewart, Charles and Berger-Wolf, Tanya and Rubenstein, Daniel I.},
  title     = {Animal population censusing at scale with citizen science and photographic identification},
  booktitle = {Proceedings of the 2017 AAAI Spring Symposium on Artificial Intelligence for the Social Good},
  pages     = {37--44},
  year      = {2017}
}
```

## License

The metadata file in this repository is released under **CC BY 4.0**. The images are **not** redistributed here; they must be obtained from WildlifeReID-10K or from the original datasets listed above, and their use is subject to the terms of those sources.
