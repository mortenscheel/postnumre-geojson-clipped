# Danske postnumre GeoJSON uden havområder

## Hvorfor?
Danske postdistrikter dækker _hele_ landet, og postnumre langs kysterne inkluderer havområder, der strækker sig helt ud til internationalt farvand.

Jeg havde brug for et GeoJSON overlay til et kort, hvor postnumrene kun dækker landområder, og som derfor inkluderer kystlinien.

## Hvordan?
Udgangspunktet er den officielle GeoJSON for danske postdistrikter fra [DAWA](http://dawa.aws.dk/), som samtidig indeholder information om, hvilke kommuner postnummeret overlapper.

Heldigvis dækker landets kommuner kun landområder, så deres geografiske definition indeholder kystlinierne.

Ved hjælp af [geojson-clipping](https://github.com/mfogel/geojson-clipping) er hvert postnummer behandlet ved at beregne _intersection_ mellem to GeoJSON polygoner:
1. Postnummeret, som inkluderer havområder.
2. De kommuner som postnummeret overlapper (kombineret til ét polygon via _union_).

Den resulterende fil fyldte næsten 300 MB (se evt. `postnumre-clipped.geojson.zip`).

Ved hjælp af [MapShaper](https://mapshaper.org/) blev denne fil simplificeret til godt 2 MB (se `postnumre-clipped-simplified.geojson`).
