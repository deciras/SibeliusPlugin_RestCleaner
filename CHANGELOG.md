# Changelog

## v1.2.0

- Added iterative rest merging, so one run continues merging until no further legal merge remains.
- Added per-bar meter detection, so mixed meter passages are processed bar by bar instead of using one global meter.
- Added rest-group rules for common meters including `2/4`, `3/4`, `4/4`, and `6/8`.
- Added conservative default handling for several odd `x/8` meters such as `5/8`, `7/8`, `11/8`, and `13/8`.
- Preserved the user's original passage selection across split and merge stages.
- Added a repository `VERSION` file and refreshed documentation.

## v1.0.0
Initial release.

Features:
- Detect illegal rests
- Split cross‑beat rests
- Merge legal rests
