# HMS-SurgVTG

HMS-SurgVTG contains natural-language queries and temporal annotations for 50 CholecT50 surgical videos. Queries cover surgical phases, instrument use within a phase, and action triplets within instrument use.

## Contents

```text
hms_surgvtg/
├── train.jsonl      # Training queries
├── val.jsonl        # Validation queries
├── test.jsonl       # Test queries
├── splits.json     # Video IDs for each split
├── categories.json # Category IDs and names
├── statistics.json # Dataset counts
├── README.md
├── NOTICE.md
└── LICENSE
```

| Split | Videos | Phase | Instrument | Triplet | Queries | Segments |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Train | 35 | 239 | 530 | 1,089 | 1,858 | 5,517 |
| Val | 5 | 32 | 61 | 134 | 227 | 633 |
| Test | 10 | 68 | 159 | 354 | 581 | 1,640 |
| Total | 50 | 339 | 750 | 1,577 | 2,666 | 7,790 |

All three video splits are disjoint. Val and test remain separate annotation files; their predictions are pooled for combined evaluation over 15 videos and 808 queries.

## Annotation format

Each JSONL line describes one query and all its matching intervals.

| Field | Description |
| --- | --- |
| `id`, `video` | Unique query ID and source video ID. |
| `query_type` | `phase`, `instrument`, or `triplet`. |
| `query`, `phase` | Query text and associated phase name. |
| `parent_id` | Parent query ID; null for phase queries. |
| `parent_segments` | Ground-truth parent intervals; null for phase queries. |
| `segments` | Matching `[start, end]` intervals in seconds. |
| `video_duration` | Video duration in seconds. |

Timestamps refer to the original video timeline at 1 FPS. Segment endpoints are the first and last annotated frame timestamps; duration is `end - start`. Category names are preserved as supplied, including `carlot-triangle-dissection`. The category mapping includes the full source taxonomy, including null categories.

## Source and video frames

The source dataset is [CholecT50](https://github.com/CAMMA-public/cholect50), provided by CAMMA, ICube, University of Strasbourg. Obtain video frames separately. Frames should retain their video IDs and zero-based indices, such as `videos/VID01/000000.png` at 1 FPS.

See [NOTICE](NOTICE.md) for attribution and [LICENSE](LICENSE) for the data terms of use.
