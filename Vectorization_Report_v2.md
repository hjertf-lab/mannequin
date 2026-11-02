# Vectorization report — revision 2 (WORKING DRAFT)

NOT APPROVED FOR PRODUCTION. Revision 1 was rejected for jagged lines, breaks and loops. Revision 2 smooths the curves but retains unresolved topology and missing strands. It does not fulfill the exact-reconstruction requirement.

Source: supplied PNG, 1024 × 1536 pixels, from Male -front för codex.zip.

## Delivered geometry

The three SVG files contain actual editable paths; there are no embedded raster images. Master has the requested six named groups, an independent closed gray silhouette, regional centerline strokes, an outer contour, and vector clipping. Background is transparent. The reference layer was omitted. All artwork retains source coordinates, pose, and proportions; no generic mesh or generated anatomy was substituted.

Wireframe: 3,693 paths, approximately 8,692 endpoint anchors. Silhouette: one closed path, approximately 629 anchors. Master includes the silhouette geometry again for its outer contour and non-visible clipping path. Bezier control handles are additional editable coordinates, not included in these anchor counts. Paths split at skeleton branches/intersections; a complete grid strand can therefore comprise several paths.

## Method

White-composite the supplied PNG for analysis; upsample 2×. In torso/legs, Gaussian-filter (sigma 0.65 upsampled pixels), threshold at 235/255 and close subpixel breaks using a 3×3 upsampled kernel. In head, hands and feet retain threshold 215/255 without closing to reduce merging of close details. This is local interpolation, not recovery of missing long strands. Extract the largest external contour, skeletonize, and trace graph edges. Collapse small duplicate arcs with identical junction endpoints only when their separation is below 2.5 source pixels; 23 pairs were collapsed in this run. Pair opposing branches at junctions when their directions agree within about 31 degrees of straight continuation. Smooth traced samples with endpoint-preserving Gaussian filtering (sigma 1.6 source pixels for broad body lines, 0.6 for details and outline). Fit cubic Beziers with tangent-constrained nonnegative handles and a 0.52-pixel tolerance to the SMOOTHED samples. Thus that tolerance is not a bound against the original raster. Uniform 0.75-pixel strokes, neutral gray fill. Spatial regional grouping remains approximate.

Revision 1 used 7,081 wireframe paths and 23,119 anchors. Revision 2 reduces that to 3,693 paths and 8,692 anchors. Fewer anchors and smoother paths do not establish correct topology.

## Validation and visual review

Rendered all SVGs with CairoSVG. Parsed all three SVGs as XML and confirmed paths exist and raster image elements are absent. Reviewed enlarged head/neck, both hands, thighs/knees, and feet. Revision 1 failed enlarged inspection in Illustrator. Revised smoothing, short-gap treatment and branch pairing have been rendered and inspected in the same hip region and the full QA sheet. Illustrator itself remains untested. Current QA and comparison correspond to the final revision.

At source resolution, 90.09% of original dark pixels (gray <170) are within one pixel of rendered wireframe dark pixels; 96.36% of rendered dark pixels are within one pixel of original dark pixels. Source-to-vector distance, 95th percentile: 2.00 pixels. These measure spatial alignment, not guaranteed topology, silhouette equivalence, or production approval. Differences in thickness and antialiasing affect the numbers.

Comparison shows original versus gray-filled master. QA includes enlarged originals, vector renders, and red/cyan alignment overlays. Full-frame overlay: red denotes source-only darkness, cyan vector-only darkness, black coincidence. Preview is a 2048 × 3072 transparent render, not additional source detail.

## Remaining imperfections and manual work

This is an automatically traced editable master requiring manual finishing before production use, not a certified exact reconstruction. Source rasterization limits recoverable detail. Visible unwanted small loops and junction distortions remain especially at the inner thighs/crotch. Some strands are missing or end abruptly, including the central pelvis line, and slight kinks remain. Smoothing reduces fine detail in dense regions; the result is not an exact vector copy. Short segments also remain at fingers, toes, ears and neck. Close parallel strokes can merge in the raster/skeleton, and faint or disconnected source segments may remain fragmented. In those regions, inspect the supplied QA and original; manually join only visually verified strands and adjust tangents/weights. The smoothed outer contour follows the observed raster approximately; fine silhouette detail is not guaranteed unchanged. Uniform strokes do not reproduce every original variation in darkness/weight. Node density is intentionally conservative to prioritize alignment. No missing geometry was silently invented.

SVG uses standard paths, cubic curves, groups, and vector clipPath. Adobe Illustrator opening/editing and layer import have NOT been tested because Illustrator is unavailable. Verify grouping, clipping and stroke appearance in Illustrator before production acceptance; named groups may import as groups rather than native Illustrator layers.

## Reproduction

Python scripts, dependency versions and source PNG are included in the ZIP under pipeline/. Run `python3 -m pip install -r requirements.txt`, then `python3 vectorize.py` and `python3 finalize.py` from the pipeline directory. Outputs go to output/. The finalization script derives its directory from its own path.
