# Compact E15.5 mouse-brain CellCloud DegaFiles

These are the same 3,787,366 cells, 43 sections, 480 genes, raw counts,
cluster labels/colors, and centroid/neighborhood alignments as the
[original dataset](../xenium_E15.5_cell_cloud/). Data generated in collaboration
with the [Allen Institute](https://alleninstitute.org/).

Positions are rounded to the nearest 1 µm. Original cell IDs occur once in
`cell_ids.parquet`; geometry, cluster, and sparse expression tables use uint32
canonical row IDs. Zstd and delta encoding reduce the data from 4.59 GB to
494 MB. The selected alignment, identities, clusters, and gene metadata for
the initial view total about 31.3 MB; gene expression downloads on demand.
Both `neighborhood` and `centroids` alignments are included.

Requires the Celldega 0.28.0/current browser reader. Earlier published bundles
that do not understand `cell_ids` cannot read this indexed layout.

```python
cloud = dega.viz.CellCloud(
    base_url="https://raw.githubusercontent.com/broadinstitute/celldega_xenium_E15.5_cell_cloud/main/xenium_E15.5_cell_cloud_compact",
    alignment="neighborhood", cluster_attr="leiden_1.0",
)
```

An equivalent [AnnData Zarr](https://huggingface.co/datasets/broadinstitute/Celldega_Supporting_Data/tree/main/Allen-Broad_Dev-Mouse-Brain/E15.5/cellcloud_v2_1um.zarr)
can be opened with `CellCloud(zarr_url=..., alignment="neighborhood", cluster_attr="leiden_1.0")`.

The compact export was validated against all source expression values, IDs,
cluster labels/palettes, and both alignment coordinate arrays. Maximum rounding
error is 0.5 µm per axis. Original files were not replaced.

Reproduce with [the preparation script](https://github.com/broadinstitute/celldega/blob/main/scripts/prepare_allen_mouse_brain_cellcloud.py).
Source AnnData: [pinned H5AD](https://huggingface.co/datasets/broadinstitute/Celldega_Supporting_Data/resolve/df537e04ad0e51a91f3d68a53b788efb61552913/Allen-Broad_Dev-Mouse-Brain/E15.5/xenium_E15.5_clustered.h5ad).
Source alignment revision: `e8d0d6fb17109333e982497fca1c526e5e457747`.
`SHA256SUMS` records the 489 data-file checksums.
