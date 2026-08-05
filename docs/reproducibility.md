# Reproducibility Notes

## Preservation policy

The six notebooks and the PyTorch checkpoint in this repository are copied from the submitted archive without modifying their contents. The repository adds documentation and organization around the original implementation rather than rewriting it.

`ORIGINAL_FILE_MANIFEST.tsv` records the SHA-256 hash of every preserved source artifact and maps its original archive path to its portfolio path.

## Data availability

The image dataset and annotation files are not included. The notebooks expect locally stored PNG/JPEG images, AnyLabeling-style JSON polygon annotations, and an `excluded.csv` file used to categorize rejected samples.

The outputs saved in the notebooks record the following dataset stages:

- 862 usable PNG images and 102 excluded PNG images after the initial split.
- 95 polish-related excluded images with annotations.
- 3,508 usable nail-only crops.
- 402 polish nail-only crops.
- 3,910 total crops used for binary classification.

These counts describe the original run and do not substitute for the private source dataset.

## Local paths

The notebooks contain the original absolute macOS paths used during development. They were intentionally left unchanged. To rerun the workflow on another machine, edit the path constants in the first configuration cell of each notebook in a local working copy.

## Suggested execution order

1. `extract_from raw_png.ipynb`
2. `excluded_class.ipynb`
3. `clean_usable_mask.ipynb`
4. `polish_mask.ipynb`
5. `03-2_train_polish_binary_classifier.ipynb`
6. `my_test.ipynb`

Run the training and inference notebooks from the `notebooks/` directory so the relative checkpoint path resolves correctly.

## Model checkpoint

`best_segmented_polish_classifier_group_split_v2.pth` is approximately 43 MiB and is configured for Git LFS through the repository's `.gitattributes` file.

Before the first commit containing the checkpoint:

```bash
git lfs install
git lfs track "*.pth"
git add .gitattributes notebooks/best_segmented_polish_classifier_group_split_v2.pth
```

## Result-version note

The presentation records an earlier experiment with 90.2% test accuracy. The final report and final training notebook record the later full-distribution result of 98.66% test accuracy. Both documents are retained as project history.
