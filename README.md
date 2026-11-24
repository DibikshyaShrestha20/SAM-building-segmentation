# SAM Building Segmentation

Automatic building extraction from aerial/drone imagery using Meta's
[Segment Anything Model (SAM)](https://github.com/facebookresearch/segment-anything),
with size/shape filtering and export to a binary mask (PNG) and polygons (GeoJSON).

[!(https://github.com/mankumarigit123)](https://colab.research.google.com/github/YOUR_USERNAME/sam-building-segmentation/blob/main/sam_building_segmentation.ipynb)

## Results

|Input|Building mask|
|-|-|
|!\[input](examples/input.png)|!\[mask](examples/building\_mask\_comparison.png)|

|All SAM masks|After filtering|
|-|-|
|!\[all](examples/all\_masks.png)|!\[filtered](examples/filtered\_masks.png)|

On the sample image (1604 × 818 px), SAM generated 582 masks; 510 remained
after filtering and 501 were exported as polygons.

## How it works

1. Load the SAM ViT-H model
2. Generate masks automatically across the whole image (`SamAutomaticMaskGenerator`)
3. Filter masks by area and aspect ratio to keep building-like objects
4. Optionally segment a single building from a point prompt (`SamPredictor`)
5. Export a combined binary mask and building polygons

## Usage

1. Click the **Open in Colab** badge above
2. Set the runtime to **GPU** (Runtime → Change runtime type)
3. Run all cells and upload your own aerial image when prompted

The model weights (\~2.4 GB) are downloaded automatically on the first run.
Use `vit\_b` or `vit\_l` in `MODEL\_TYPE` for a smaller, faster model.

## Outputs

* `building\_mask.png`: combined binary building mask
* `buildings.geojson`: building polygons

## Limitations

* The GeoJSON is in **pixel coordinates** with no CRS. For real-world positions
in QGIS, run the pipeline on a georeferenced GeoTIFF and transform the
coordinates with `rasterio`.
* Filtering is size/shape based, so non-building objects (e.g. courtyards,
roads) can pass through. Tune the parameters per image.

## Credits

Built with [Segment Anything](https://github.com/facebookresearch/segment-anything) (Apache 2.0).

## License

MIT, see [LICENSE](LICENSE).

