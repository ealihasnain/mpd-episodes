# MPD Episodes

Per-episode production artifacts for the YouTube channel
[@moneypatternsdecoded](https://youtube.com/@moneypatternsdecoded).

Each episode lives in its own folder `D###_TopicShort/` containing the
text-based pipeline artifacts:

```
D###_TopicShort/
  index.md                    # current artifact URLs + versions (fetched by mpd-producer)
  01_StrategyBrief_v#.html
  02_VoiceScript_v#.html
  05_Captions_v#.srt
  05_Captions_v#.json         # word-level alignment
  06_VideoHTML_v#.html
  09_Thumbnail_v#.png
  10_UploadPack_v#.html
```

Audio masters (`.mp3`) and the final video master (`.mp4`) live in the
producer's local workspace only — too large for git, and the producer
doesn't need to `web_fetch` them during the chat-only pipeline.

## How `mpd-producer` finds episode artifacts

The `mpd-producer` skill bootstraps from the master manifest at
[`ealihasnain/mpd-knowledge/manifest.md`](https://github.com/ealihasnain/mpd-knowledge/blob/main/manifest.md),
which contains a URL list of every active episode's `index.md`. Fetching
an `index.md` unlocks `web_fetch` on its listed artifact URLs, allowing
downstream stages to ingest the outputs of prior stages across chat
boundaries.

## Adding a new episode

1. Create folder `D###_TopicShort/` here.
2. Drop initial artifact + `index.md` (URL list for that episode).
3. Commit + push.
4. In `mpd-knowledge` repo, append the index URL to the manifest's
   Episodes section.
5. Commit + push manifest.

## License

MIT — see [LICENSE](LICENSE) if present, else default MIT terms apply.
