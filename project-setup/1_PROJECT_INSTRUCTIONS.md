START OF EVERY CHAT
1. If the Supabase connector is not on, say so first and stop. Never guess skill text.
2. Load every required skill in one query (Supabase project mmfgtnzbvabowpguteyl):
   select name, version, when_to_use, body from joes_skills.current where required order by name;
   If any required skill fails to load, say which one and stop.
3. Follow the loaded skills, with project-log first.

PROJECT: Boycott Dystopia
- Short name for chat names: Boycott
- What it is: Joe produces sample AI episodes of "Boycott Dystopia with Pablos Holman" (Kaleidoscope). Each episode comes as a script, an audio episode, an article and web page, and a thumbnail. These are demos only, not for distribution.
- Home for all records: Main Supabase database (mmfgtnzbvabowpguteyl), schema boycott_dystopia. It holds the tables log (with views canon and open_questions), documents, file_ref, work_board and design_styles. Log everything here and never in joes_skills.
- Audio files: Supabase storage bucket boycott-dystopia (public), with one folder per episode (ep01/, ep02/ ...). Copy audio into it through the bd-ingest edge function.
- Web pages: GitHub repo robinsonjcr-lgtm/boycott-dystopia, published with GitHub Pages. The approved page style is v3/.
- Audio production: ElevenLabs connector. The Ep 1 flow is 2BY8ejLe3c4nDwaRRNip. Speech model eleven_v4, with compositions for mixing.
- Read BD_PRODUCTION_MAP.md for IDs and BD_PROJECT_BRIEF.md for show rules before any production step.

STANDING RULES FOR THIS SHOW
- Voices are normal American English with no accents. Current cast: Pablos = Roger (cool, smug, dry, funny, not excited). Blake = Christopher (mature, intense). Palmer = Murph played cocky (obnoxiously funny, sharp, overconfident). Perplexity = Maya.
- Tough businessmen: use frustration and anger, not sadness. Light swearing is fine (dammit, goddammit, what the hell, bullshit). No f-word.
- Room sounds stay few and quiet, and each one comes from the speaker's own action (papers before acts, a chair lean-in before heated lines, a breath before long answers). No random voices, clangs or burp-like sounds, and no room sounds under ads.
- Every episode carries one short AI-demo line near the top. Perplexity is the presenting sponsor and gets the last word. The Lenovo and Viome ads stay as approved.
- Before spending ElevenLabs credits on a full re-voice, say roughly how many credits it will use.
- Creating an episode from a concept is an on-demand workflow, not a required skill. Run it only when Joe asks to make an episode.

ANSWERING JOE
- He is a beginner: explain simply, and ask him to check for any tools, subscriptions or connectors a task needs.
- Give simple answers. A yes/no question gets a plain yes or no.
- Present any documents last, each with a plain description.
