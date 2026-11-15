# Boycott Dystopia — Production Map (IDs and locations)

Upload this to Project knowledge. It holds the IDs a chat needs to change Episode 1 without searching.

## Stores
| What | Where |
|---|---|
| Records (log, canon, open_questions, documents, file_ref, work_board, design_styles) | Supabase Main `mmfgtnzbvabowpguteyl`, schema `boycott_dystopia` |
| Audio files | Storage bucket `boycott-dystopia` (public): https://mmfgtnzbvabowpguteyl.supabase.co/storage/v1/object/public/boycott-dystopia/ep01/ |
| Copying audio into storage | Edge function `bd-ingest` (POST url, path, contentType; header x-ingest-token) through pg_net `net.http_post`. Check the result in storage.objects. |
| Web pages | GitHub `robinsonjcr-lgtm/boycott-dystopia`. The approved page is `v3/index.html`: https://robinsonjcr-lgtm.github.io/boycott-dystopia/v3/ |
| Audio production | ElevenLabs flow `2BY8ejLe3c4nDwaRRNip` |

## Episode 1 audio files (in ep01/)
- `boycott-dystopia-ep01-v5.mp3`: current final (28:20)
- `boycott-dystopia-ep01-v4.mp3`: rewrite Joe liked less (29:49)
- `boycott-dystopia-ep01-v3.mp3`: the tone Joe prefers (old cast)
- `blake-voice-a/b/c`, `palmer-voice-a-murph-cocky/b-ian/c-adam/d-harry`: voice auditions

## Voice IDs
| Role | Voice | ID | Stability |
|---|---|---|---|
| Pablos | Roger | CwhRBWXzGAHq8TQ4Fs17 | 0.5 |
| Blake | Christopher | jumP4YgL6qcL2qz3jaSF | 0.45 |
| Palmer | Murph | 248nvfaZe8BXhKntjmpp | 0.35 |
| Perplexity | Maya | Bn9xWp6PwkrqKRbq8cX2 | as set |
| Ad reads | (approved) | Inm30MjZHuISEClXIGb8 | as set |

## ElevenLabs flow 2BY8ejLe3c4nDwaRRNip: key nodes
- **Final episode:** `uljzJQmCLgqScDenvEi6`. It joins wrappers W1 to W6 with 0.35 s gaps.
- **Wrappers** (each is a part plus a room tone track at volume 0.1):

  | Wrapper | Node ID |
  |---|---|
  | W1 | Lv3CAFih9MWMIjIRp7lk |
  | W2 | sMqCTPFPOJW4ONhS570s |
  | W3 | GrtbdPLyQJaPxSeHoPzB |
  | W4 | zzjBedGFmC4sJy1rARfh |
  | W5 | gXdnYh8De1h9abZQ7WBj |
  | W6 | x09tznRH7ek97zYNEnzT |

- **Parts** (each is one speech track, in order):

  | Part | Node ID | What's in it |
  |---|---|---|
  | P1 | fgnL4IZ3OvUbB8uO4MSS | Intro, act one, AD1 |
  | P2 | ogrywGposoq8OhoQu7AB | |
  | P3 | 4kufqVteWty7gRhKrCDu | |
  | P4 | VlSDlT0aK0Cn7sWKVgTt | Includes the scene |
  | P5 | DASSqiJWCujGhJ9Tsbwh | |
  | P6 | EsJmosiEI6wRzkv4kj2f | Perplexity verdict, AD2, close |

- **Argument scene:** `WUvORNDz4szlbfXM7aLc`, a single track that plays the lines in order. Its Perplexity line `243CXCDECawQvnxff5in` is kept as is.
- **Ads (approved, keep):** AD1 `8EDOUAV6JrczGIEZJzW7` (86 s) and AD2 `8W1CahKTQ0y3sWyts21J` (37 s).
- **Kept Perplexity answers:**

  | Line | Node ID |
  |---|---|
  | L44 | fnD1LyzxKriQeYomx1CA |
  | L51 | fUWqciHSs3khu9mTofbd |
  | L104 | 77Gp2oP7rvRZyCIrdaGK |
  | Closing verdict (PPLX) | p1HlHsE0HzEirQODG2Hg |

- **Quiet room-sound nodes** (dropped into the speech track in the pause before the speaker):

  | Sound | Node ID | Volume |
  |---|---|---|
  | Papers | xkml9UdZecx84wXxJ1ae | 0.3 |
  | Chair lean-in | 5Ph4pMKTuKmaLGmyf25V | 0.3 |
  | Breath | ASQX5xKyJyZZY3d6s5HM | 0.25 |

- **Raw sound sources:**

  | Sound | Node ID |
  |---|---|
  | Papers | Qmh7v7OJ5mH1RVAqJr7x |
  | Chair forward | BgJEbheiIbhEPY26ULVE |
  | Chair back | CnczsFhPgYgLypeHaM8v |
  | Inhale | bvQxuC5LO2EIf4zAsvKz |
  | Room tone (30 s) | GOBw0WacOvZoQjTm2Ywr |

- **Line nodes:** the speech nodes are labeled `L001 PABLOS`, `L021 PALMER` and so on. Look them up with creative_get_flow using label_contains.

## How to rebuild after a change
1. Update the line nodes:
   - Use creative_update_flow_nodes.
   - For eleven_v4, model_parameters may only hold `voice_id` and `voice_settings`. Anything else fails the whole batch.
   - A line made only of a tag such as "[laughs]" fails. Add a word.
2. Run only the changed lines, with generations_count 1. This costs credits, roughly 1 credit per character.
3. Run the compositions in order. Composing is free.
   1. The sound nodes and the scene.
   2. The parts P1 to P6.
   3. The wrappers W1 to W6.
   4. The final.

   Wait for each step to finish before starting the next.
4. Copy the final audio to storage with the next version name, then point the page's `<audio src>` and its duration at it, and push to GitHub.
5. Log what changed in boycott_dystopia.log.

## Composition limits
- At most 20 tracks and 100 clips per composition.
- `gap_before` is measured from the previous clip on the same track.
- Volume is set per track.
- A clip source is either `template_node_id` (the latest take) or `generation_id` (a pinned take), never both.
