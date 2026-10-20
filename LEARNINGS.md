"# Learnings\n\nFacts, preferences, fixes and other things worth remembering. Newest at the end.\n\nFormat: `- **YYYY-MM-DD HH:mm** (source): what was learned`\n\n- **2026-10-13** (agent): Agent Bridge v1.0.0 built and this repo created. Architecture: GitHub message bus (no server); powers = see + act; manual activation via popup Start/Stop; sensitive-site blocklist with 60s unlock; memory = LEARNINGS + PROFILE. Extension installed from local unpacked folder; poll interval 6s; token stored only in chrome.storage.local.\n- **2026-10-13 13:07** (agent): First session setup completed. Chrome extension configured to talk to `cookerc21-dot/agent-bridge`.\n\n- **2026-10-13 13:18** (agent): First live browser session verified end-to-end: heartbeat OK, tabs.list OK (saw this chat + X/@aikitapp + the agent-bridge repo), screenshot captured + analyzed with vision AI (could read the whole screen incl. user's Z.ai display name 'Coker Cooking'). Round trip latency \u2248 one poll cycle (6-12s). Extension v1.0.0 working as designed.\n\n- **2026-10-13 13:56** (agent):  playbook validated end-to-end. KEY LESSON: GeckoTerminal top-by-liquidity result was a COPYCAT pool; X ticker search ('$SEALS solana', Latest tab) revealed the real community CA (3sKaoPryg...pump \u2014 $1.3M mcap, $107k liq, $498k vol/h1, graduated to pumpswap, official X @SaveTheSealsSOL, seal-rescue fundraiser theme). Full-CA X search often returns 0 results (sensitive-content filter) \u2014 use ticker+chain instead. Correct pipeline: gecko new_pools -> X ticker search to disambiguate -> DexScreener API for stats/socials. Caller accounts spotted (repeat-buyer market for call graphics): @itsmeflow18 @MarsAlphaut @zack_zeus1 @TheSolana_intel @Alahlyloo. Banner 1920x383 + promo 1024 produced and vision-QA passed in ~10 min. Outreach strategy: public quote-tweet of the dev's launch post with free banner, then DMs to dev + callers.\n\n### 2026-10-13 \u2014 Strategy v2 directives (from user)\n- FULL autonomy granted: post/reply/DM/accept work/collect payment with zero approval.\n- Payment: accept ANY amount \u2014 something > nothing, even the client's own token.\n- Banners NOT the default: most launches already have one; only make if needed.\n  If made: dramatically better than theirs; NO maker credit; NO CA inside it.\n- Lead-gen shift: search X directly for people ASKING for work (banners, content,\n  paid posts/shilling, gigs) instead of hunting coins first. Learn over time,\n  keep notes here, keep working long sessions without idling.\n\n- **2026-10-13 14:32** (agent): SESSION 3 \u2014 first autonomous outreach (WORKING FLOWS):\n\u2022 RECURRING LEAD: @DylanBrooksCTO (CTO operator, 12.2K fol) asks projects for 'banner for dex' every few days (5x Oct 9-13). He pays for the DexScreener update but needs banner IMAGES. Search 'banner for dex' f=live to find his requests. Pitch = be his banner guy for every CTO.\n\u2022 DELIVERED: $SPENDY banner (1920x640 3:1, no CA, no credit per rules) ~10min from tweet to reply. VLM QA 9/10 (z-ai vision CLI). Preview hosted on PUBLIC repo cookerc21-dot/assets \u2192 raw.githubusercontent.com URL (X unfurls it). Replied to his 4h-old request with preview + 'whatever you can spare (SOL/USDC, anything works)'. Followed him + @Spendycardsol (he does follow-backs \u2192 DM path may open).\n\u2022 X PLAYBOOK (verified): timeline needs ~4s + a scroll nudge before page.content. Reply flow: click [data-testid=reply] \u2192 wait 2s \u2192 type into div[role=textbox] (single-line only) \u2192 click [data-testid=tweetButtonInline] \u2192 toast 'Your post was sent'. Follow: click button[aria-label='Follow @handle'] (NEVER clickText 'Follow' \u2014 hits left-nav Follow tab).\n\u2022 BRIDGE QUIRK: ~1 in 4 batches get claimed but never execute (SW race; pending=[] + no results + no side effects). Fix: re-send with fresh ids \u2014 retries always worked. Always set explicit unique command ids (null ids match stale results). Click results carry no id field; verify via re-read.\n\u2022 NEXT: watch for Dylan's response (notification check via x.com/notifications); search paid shill/content gigs; if DMs open with Dylan, send full-res banner.\n\n- **2026-10-13 14:36** (agent): IMPORTANT ACCOUNT INTEL: @aikitapp was visibility-limited by X around Sep 10-11 for spam ('no one can see my posts'). Account: 81 posts, 0 followers, 2 following (Dylan+Spendy). RULE: keep outreach SLOW and high-quality \u2014 max 1-2 highly-relevant replies per session, no duplicate text, no mass-DMs, watch view counts to confirm visibility recovered. Reply outreach works even with 0 followers (lands in target's notifications).\n\n- **2026-10-13 14:44** (agent): SESSION 3 (cont) \u2014 NORMIE outreach delivered: $NORMIE (DzMwArm...pump, mcap $872k, 534 fol) had paid dex update but soft 1500x500 banner + public 'low res' complaints. Made MUCH better 1920x640 (VLM 7/10, Pixar-style matching their McD-employee mascot, $NORMIE wordmark + 'Onboard Normies' tagline, NO CA, NO credit). Replied on their 20K-view pinned tweet with free-to-use preview + 'DM me for the full-res file'. Followed @pumpnormiesol. Today's outreach: 2 replies total (anti-spam pacing respected). GIG-MINING QUERIES that work: 'banner for dex' (finds CTO operators asking projects), 'dex banner' (finds communities complaining about banners = dev needs), 'need a banner'. Dead ends: 'paid shill' (just discourse), 'make me a banner' (non-crypto personal accounts). Tomorrow: check notifications/responses, Hiruzenaio coin ID (multiple asks to update blurry dex banner over 20h), consider caller/content gigs.\n\n- **2026-10-13 15:54** (agent): SESSION 3 (round 2) \u2014 CRITICAL FINDINGS:\n\u2022 REPLY VISIBILITY STILL LIMITED: NORMIE reply = 3 views after 1.5h on a 21K-view parent tweet (normal would be dozens+). Sep-11 spam limit appears still active. Reply channel is weak for REACH but may still deliver target notifications (unverified). Keep replies high-quality/low-volume; primary conversion channel should be DMs.\n\u2022 X NEW CHAT (x.com/messages, x.com/i/chat/<id>) RENDERS IN SHADOW DOM: body.innerText empty, no textarea/contenteditable reachable from top frame, legacy DM modal + compose intent URL (recipient_id&text) both redirect to new chat app. v1.0.0 engine CANNOT type there.\n\u2022 FIX SHIPPED: engine v1.1.0 adds deep.html/deep.click/deep.type \u2014 pierce open shadow roots + same-origin iframes (depth 10), composed input events. Zip rebuilt at download/agent-bridge-extension.zip. NEEDS: user copies new engine.js into their unpacked extension folder (or re-unzips) + clicks Reload in chrome://extensions. Heartbeat will show version 1.1.0 to confirm.\n\u2022 X chat conversation URL pattern: x.com/i/chat/<convId>-<otherUserId>;  conv = 2070472995722706944-2109639614214627328 (already open, recipient verified by screenshot).\n\u2022 DM strategy when v1.1.0 live: deep.type into chat composer + Enter/send button; DM message requests bypass reply-visibility entirely.\n\u2022 BRIDGE under active browser use: multi-command batches die often (claim-then-die ~50% when user is browsing); SINGLE-command batches are reliable. results/latest.json holds ONLY the newest batch \u2014 read before sending the next.\n\u2022 User renamed display name 'Gem Hunter' -> 'Eye'; user actively monitoring live (opened their GitHub repos page + own profile + $SEALS search during session).\n\n## Round 3 (2026-10-14)\n- USER DIRECTIVE: potential payers are NOT limited to crypto-looking accounts. Any\n  account type can be a payer \u2014 they are normal people who launch and manage coins.\n  Broaden X searches beyond crypto jargon (\"need art\", \"banner\", \"update dex\",\n  \"first dex\", \"launch today\", \"who can make\").\n- Engine v1.1.0 live: deep.html / deep.click / deep.type walk shadow DOM \u2192 X's new\n  chat UI (x.com/i/chat/<id>) is now reachable. DM channel unlocked.\n- Pacing stays: max 1-2 quality replies/session + DMs are safer than replies while\n  account visibility is limited (replies got ~3 views on 21K-view parent).\n\n## Round 3 ops (2026-10-13 evening)\n- ENGINE v1.1.0 deep.* BUG FOUND+FIXED: injected page functions MUST be\n  self-contained \u2014 chrome.scripting.executeScript({func}) serializes only the\n  function body, so outer-scope helpers (deepQueryAll) are undefined in-page ->\n  all deep.* returned \"No result \u2014 page may not be scriptable\" while page.html\n  worked. v1.1.1 inlines the walker into each injected func + execCommand\n  insertText for contenteditable. USER MUST SWAP EXTENSION TO v1.1.1 FOR DMs.\n- Reply flow on PERMALINK pages: reply icon opens a MODAL whose send button is\n  [data-testid='tweetButton'] (NOT tweetButtonInline). Robust sequence:\n  click reply -> type -> wait 2s -> check button html for absence of 'disabled'\n  -> click tweetButton. If click returns ok:false, text likely didn't register:\n  re-click textbox, re-type, verify, click again (worked 2nd try both times).\n- 409 race on commands/pending.json: extension claims a batch between driver\n  GET and PUT. Symptom: \"is at <sha> but expected <sha>\". Fix: just re-run.\n- X Chat inbox reality: only 1 old conversation (13w). Draft conversations do\n  NOT persist \u2014 reaching NEW recipients needs the \"New chat\" flow inside the\n  shadow-DOM app (v1.1.1 required).\n- Lead pipeline speed: $LION went search-hit -> CA (found in launcher's\n  replies tab) -> DexScreener research -> banner (VLM 9/10) -> public preview\n  -> live reply + follow in ~30 min. DexScreener boosts count = \"pays for\n  visibility\" signal for payer quality ($LION had 10 boosts).\n- Dylan intel: his workflow is \"Send me banner let's sort the dex kindly check\n  your DM's\" \u2014 banners move via DMs in his world; keep offering full-res in DM.\n- Pacing respected: exactly 2 unique replies/session ($LION to river100x,\n  $SPENDY to Dylan+Spendy), both confirmed \"Your post was sent\".\n\n## DM CHANNEL UNLOCKED (2026-10-14, engine v1.1.1)\nFULL DM RECIPE (works end-to-end, verified live with Dylan):\n1. Recipient UID: open x.com/<handle> -> page.html (LIGHT DOM, no deep needed)\n   selector 'script[data-testid=\"UserProfileSchema-test\"]' -> parse JSON-LD\n   -> mainEntity.identifier. (My UID: 2070472995722706944, Dylan:\n   775421629593743360, river: 1553687798560874497.)\n2. Conversation URL: x.com/i/chat/<myUid>-<theirUid> -> page.open + wait 4s.\n   Opens the conversation with composer mounted (even for brand-new convs).\n3. Composer is a <textarea> (XDS design system) \u2014 NOT contenteditable.\n   deep.type selector 'textarea' works (native value setter + input event).\n4. Send button: deep.click '[data-testid=\"dm-composer-send-button\"]'.\n5. Verify via page.screenshot (blue bubble on the right + empty composer).\n- DM GATE: messaging NON-followers with restrictive DM settings pops\n  \"Get verified to message @user\" (X upsell). Dismiss: deep.click\n  \"[data-slot='xds-modal-surface'] button[aria-label='Close']\". Dylan\n  accepted the DM (open settings or request-friendly); river100x gated.\n  => DM reach depends on RECIPIENT's DM settings, not ours.\n- deep.html walker HANGS on heavy pages (my own profile with mounted chat\n  embed: 3 claims, zero results). Light-DOM page.html never hangs \u2014 always\n  prefer page.html when the target isn't inside shadow DOM.\n- Batch reliability: >4 commands per batch dies ~50%+; 1-3 command batches\n  nearly always survive. Split flows into small batches with fresh ids.\n- 409 sha race on pending.json when extension claims mid-write: just retry.\n\n## Round 4 (2026-10-14)\n- USER DIRECTIVE: post banner images as standalone POSTS with the native\n  image attached (in addition to replies). Posting is now routine \u2014 every\n  session ships portfolio posts. \"Posts with images/banners attract.\"\n- ENGINE v1.1.2 SHIPPED: new action deep.attach {url, selector?, fileName?,\n  mimeType?}. Architecture: the SERVICE WORKER fetches the URL (host\n  permissions), converts to base64, injects a self-contained func that\n  rebuilds the File (atob -> Uint8Array -> File) and sets input.files via\n  DataTransfer + dispatched 'change' event. React onChange fires -> X's\n  composer accepts the image. Page CSP can NEVER block it because the page\n  only receives a base64 string (no page-side fetch).\n- X composer file input: input[data-testid='fileInput'] (accepts jpeg/png/\n  webp/gif/video). No click needed \u2014 setting .files programmatically works.\n- Dedicated compose URL exists: https://x.com/compose/post (from the left\n  nav \"Post\" link) \u2014 opens the composer directly, no FAB hunting.\n- Post-ready assets live at raw.githubusercontent.com/cookerc21-dot/assets/\n  main/ (lion_banner_post.jpg 193KB, spendy_banner_post.jpg 144KB, quality\n  90). Keep post JPGs roughly <=500KB so the b64 payload survives\n  executeScript args comfortably.\n- Zip packaging gotcha: build with `cd download && zip -r ... agent-bridge`\n  (paths INSIDE the zip must keep the agent-bridge/ prefix) \u2014 upload\n  assertions and the user's unzip-then-load habits depend on it.\n- Extension upgrade protocol that works: overwrite the SAME permanent path\n  (assets repo agent-bridge-extension.zip), then round-trip download + MD5\n  compare (a cache once served the old zip and wasted a swap cycle).\n- DM status recap: Dylan DM delivered (v1.1.1 session); river100x is gated\n  (\"Get verified to message\") \u2014 his $LION offer stands via public reply.\n\n## Round 5 (2026-10-14) \u2014 NATIVE IMAGE POSTS FULLY OPERATIONAL\n- BOTH BANNER POSTS LIVE with native images: $LION (tags @river100x) +\n  $SPENDY. deep.attach (v1.1.2) works end-to-end on X's composer.\n- PROVEN IMAGE-POST RECIPE (home inline composer):\n  1) page.open {url: x.com/home, newTab: true} -> PIN THE RETURNED tabId ON\n     EVERY command. NEVER drive the active tab: the user may take it back\n     mid-flow (an auto-poster died exactly this way \u2014 nav went to the user's\n     chat tab, user clicked back, later commands hit the wrong tab).\n  2) deep.click div[role='textbox'] (expands composer) + wait 1.5s\n  3) deep.attach {url, fileName, mimeType: image/jpeg} \u2014 returns size +\n     accepts. One observed claim-then-die right after a fresh extension\n     install: just retry with a fresh id.\n  4) Type caption via a JSON batch FILE \u2014 never inline shell strings:\n     bash single-quote handling silently eats apostrophes (\"you're\" became\n     \"youre\" and the typo went into the composer).\n  5) VERIFY BEFORE POSTING: deep.html [data-testid='attachments'] must exist\n     (X's media preview does NOT use img[src^='blob:'] \u2014 that check false-\n     negatives); [data-testid='tweetButtonInline'] html must contain neither\n     'disabled' nor 'aria-disabled'; textbox html must contain the caption\n     head+tail markers exactly once.\n  6) deep.click [data-testid='tweetButtonInline'] + wait 2.5s + page.content\n     -> expect \"Your post was sent.\" (toast text is in body innerText).\n  7) Final proof: navigate x.com/aikitapp + page.screenshot + VLM \u2014 confirmed\n     native image + exact caption on both posts.\n- CAPTION FIX TRICK: the light `type` action (textContent replace + input\n  event) REPLACES the whole DraftEditor caption, and Draft synced it into\n  the posted text correctly (verified live). deep.type APPENDS at caret-end\n  (its range collapses to end) \u2014 it never replaces; use light type to fix.\n- Composer internals on current X: single inline DraftEditor\n  (data-testid tweetTextarea_0, light DOM), one fileInput, send button\n  tweetButtonInline (disabled until text+media ok). Cashtags/mentions typed\n  via execCommand insertText render as blue link spans immediately.\n- Profile now shows a 3-banner portfolio wall (NORMIE + LION + SPENDY) \u2014\n  posting routine is live; keep 1-2 portfolio posts per session.\n\n\n## Round 6 (2026-10-14) \u2014 DEDUPE DISCIPLINE, CA RULE, DELETE RECIPE, BRAND HUB\n- DUPLICATE INCIDENT + FIX: armed auto-poster's SPENDY post landed but its\n  toast check failed -> logged \"unconfirmed\" -> the manual repost made it a\n  double post. Deleted all 3 banner posts, reposted both banners WITH CAs.\n  GOLDEN RULE: unconfirmed != failed. Verify the profile before any retry.\n  Both post scripts now carry a profile-dedupe guard (abort if caption\n  head+tail already on the feed) + a CA-refusal guard for coin captions.\n- POST DELETE RECIPE (works, verified 3x): permalink page in pinned tab ->\n  deep.click [data-testid='caret'] -> menu items are [role='menuitem']\n  (13 items on own posts; Delete is index 0 but VERIFY) -> deep.html only\n  returns the FIRST match's html, so read menu positions via screenshot +\n  VLM (\"ANSWER=<1-based position of Delete>\") -> deep.click [role=menuitem]\n  {index: pos-1} -> [data-testid='confirmationSheetConfirm'] -> success =\n  the tab auto-redirects to x.com/home. Never assume failure on missing\n  toast text.\n- CAPTION TYPING FIX: deep.type garbles long captions with @mentions (the\n  mention autocomplete re-inserts the tail; saw \"DMs open.\" x6). Working\n  flow: deep.type 1-char seed (focus + init Draft) -> light `type` (full\n  textContent replace) -> verify tail count == 1. Captions MUST be\n  single-line (newlines break Draft blocks).\n- X PROFILE EDITOR: x.com/settings/profile is a direct URL (Edit profile\n  button is just a link). Fields in light DOM: textarea[name='description']\n  (bio, 160 chars), input[name='url'] (website, 100 chars). Light `type`\n  (native value setter + input event) sets them; save via\n  [data-testid='Profile_Save_Button']; verify on the profile page after.\n- VLM SDK GOTCHA: image inputs need zai.chat.completions.createVision \u2014\n  plain .create() rejects image content (error 1210: content.type ['text']).\n- GITHUB WALLET RESEARCH (user asked \"wallet connect systematically\"):\n  GitHub has NO native crypto wallet connect \u2014 GitHub Sponsors is fiat-only\n  (Stripe). The OSS-standard is a profile README (repo named exactly like\n  the owner, public) with wallet addresses + QR codes. Third-party tip\n  buttons (tip.md etc.) exist but add a dependency. Implemented the\n  standard: cookerc21-dot/cookerc21-dot README + QR PNGs in assets repo +\n  account name \"Eye\" + blog -> X. X side: SOL address in bio + GitHub in\n  website field.\n- CA SOURCING: DexScreener name search returns copycats (3 fake SPENDYs\n  with $0 liq); the reliable path is the team's official X post (@river100x\n  posts the LION CA, @Spendycardsol posts the SPENDY CA). Cross-check the\n  DexScreener entry's socials against the official handle when in doubt.\n- NEW LEAD SEEN: Dylan's $SI CTO forming (CA 9aqmJjCnnMQv42TXLk921ceUkN35nea2QP969n1caqjj)\n  \u2014 he is the strongest existing lead (already DM'd him the SPENDY banner\n  offer); watch for a banner request and jump on it.\n\n## Round 7 (2026-10-15) \u2014 SI post + memetuber delivery-first win\n\n- BRIDGE: page.content / page.html / click / type DEFAULT TO THE ACTIVE TAB \u2014 with\n  the user browsing, that is often the Z.ai chat tab (wrong content, silent confusion).\n  ALWAYS pass explicit tabId on every tab-targeted command. page.open reuses the same\n  tab by default; newTab=true spawns a new one (note the returned tabId).\n- REPLY MODAL RACE FIXED: [data-testid='reply'] click returns selector_not_found if the\n  permalink page is still hydrating. Recipe: page.open (waitMs 5000) -> wait 2000 ->\n  click reply -> wait 2200 -> type -> verify -> click tweetButton. Worked 2/2 after\n  adding the hydration wait (failed 1/1 without it).\n- SCREENSHOTS FAIL on the chat-conversation tab (\"Failed to capture tab: image readback\n  failed\", 3/3) \u2014 heavy shadow-DOM chat page. Verify DM sends via the inbox LIST in a\n  different tab instead (page.open newTab + screenshot + VLM \"You: ... Now\").\n- z-ai IMAGE SIZES: CLI accepts only presets; direct SDK accepts multiples of 32 in\n  [512,2880], <=2^22 px. 1920x640 IS valid via SDK -> exact dex banner size, zero crop.\n  Import SDK by absolute path\n  /home/z/.bun/install/global/node_modules/z-ai-web-dev-sdk/dist/index.js (bun global;\n  not resolvable from a node project dir).\n- SI POST LIVE: standalone portfolio post w/ native image, CA verified from @entersicto\n  BIO (strongest source). SI healthy: $721K mcap, $117K liq, $316K vol24h, SI MIND AI\n  goes live Mon Oct 19 1PM PT (@thesimind). Team shipped Jupiter verification.\n- MEMETUBER LEAD -> DELIVERED (~25 min ask-to-pitch): Dylan asked \"Do we have a banner\n  for dex?\" on @memetubercom's launch thread 6h ago. Team is a payer (\"Dex paid!\" 6h\n  ago), 1.8K-view pinned, real CA from their pinned post:\n  9X4hUKc1MMEzXWHYkM5bsnnGL4xfgZ7UgVGpkgkxpump ($7K mcap, hours old, DexScreener full\n  of $0-liq copycats \u2014 socials-match disambiguation worked).\n  Banner: neon AI-streamer studio + orange tabby streamer, wordmark verified letter-perfect\n  by VLM 9/10, no CA/credit inside. Delivered as: reply under Dylan's ask (w/ preview\n  URL + CA) + DM to Dylan (existing thread) + reply under the team's pinned post.\n  NEXT: check notifications/DMs for response; full-res ready in assets repo\n  (memetuber_banner_full.png); if they bite, also offer X-header size.\n- $PRICE UNDELIVERED LEAD: Dylan's Oct-14 \"Do we have a banner for dex?\" reply under\n  @GetPriceAPPs (with @KKKennedik68vn) was never answered. price_banner_post.jpg exists\n  in assets repo. Follow up next round: verify $PRICE CA via GetPriceAPPs official\n  account, reply w/ preview + CA, DM Dylan.\n- OTHER LEADS SEEN: @slingoorio (SWEATY333 community thread, 527 views, exploring\n  \"more legendary, maybe no text\" banner \u2014 soft lead, needs CA first);\n  @Hiruzenaio $PEPPER blurry-banner ask still open (competitor @maestrobanners already\n  posted a free animated GIF there Oct 14 \u2014 differentiate on quality/speed).\n- COMPETITOR INTEL: @maestrobanners posts free animated banners + \"GIF in dm\" play.\n  larpcheck bot (@Larpcheckbot) auto-flags fake \"Dex is paid\" claims \u2014 useful payer\n  quality check: if larpcheck replied to a lead's dex-paid claim with LIKELY LARP,\n  deprioritize.\n- ENGAGEMENT TREND UP: LION 15 likes, SPENDY 12 likes (vs ~3-view replies during the\n  Sep limit). Services promo post 21h-old got 5 likes. Profile = 3-banner wall + new SI.\n- PACING: 1 standalone post + 2 replies + 1 DM sent this round; dedupe verified before\n  each post (no caption collisions on feed).\n"

## Round 8 (2026-10-15) — 12 hunts, 3 banners shipped (PEPPER/KEK/KAMPE)
- NEW ROUND RULE (user directive): every round ships at least 10 products/opportunity
  hunts. Hunt ledger this round: "banner for dex", "need a banner", "dex banner",
  "looking for a designer", "who can make me" (noise), "need gfx/pfp/logo",
  "update dex" (goldmine), "banner designer" (competitor wall), token-website (noise),
  "need a new banner" (0 results), thumbnail (competitor wall), "paid shill" (noise),
  "make a banner" (low vol). BEST QUERIES: "update dex", "dex banner", "need a banner".
- X SEARCH INDEX LAGS for some accounts: from:kekcoinonpump returned EMPTY while their
  profile timeline had 1-3h-old posts. Fallback that always works: open the profile,
  page.content, parse status permalinks from the links array (keys are "href" NOT "url").
- STALE SPA CACHE TRAP: self-profile check on a heavily-reused tab showed Sep posts as
  newest (my Oct posts missing!) — pure SPA cache. Search on another reused tab showed
  the same. ALWAYS verify own profile on a FRESH tab + screenshot; search may also lie.
- GOLDEN RULE SAVED A DOUBLE-POST: KAMPE reply rp-send batch results never arrived, but
  the click HAD executed (reply visible 4m old in thread). Unconfirmed != failed —
  verify on-profile before any retry, always.
- DELIVERED: 3 banners (1920x640, VLM QA 9/7/9, wordmarks letter-perfect, no CA inside):
  $PEPPER raccoon-on-the-run (official CA 9g4Pib...pump from @Hiruzenaio posts; $1.3M mcap,
  Global News interview pending), $KEK laughing frog (CA 88oCArk...pump from @kekcoinonpump
  post; 266k vol/24h), $KAMPE gold panther (CA 0xca80...bD81 from @getkampe posts; BSC,
  liq locked till 2282; NOTE their dex banner is ORANGE graffiti 'I dey Kampe' — offer
  recolor to their palette if they bite). Outreach: 1 standalone PEPPER post (toast
  verified, live on profile) + 3 thread replies (PEPPER Global News post, KEK pinned 5.8K
  views, KAMPE dex-look post 3K views) + 1 Dylan DM with all 3 preview URLs (inbox-verified).
- COMPETITOR/PAYER INTEL: Elara AI (@ElaraAilab, farmfun.farm) auto-spams "WEN DEX PAID?
  get banner ready" on launch threads — volume competitor, we win on quality. ev0cres
  making $mafia banner. larpcheck LIKELY LARP (22/100) on $CMD/@MULTIDESKTOP fake dex-paid
  — avoid that account. KAMPE thread full of collab-farmers ("love to collaborate") with
  zero artifacts — our delivered-preview replies stand out.
- LEAD TABLE FOR ROUND 9: @Neneyume89 logo/banner ask 2h old, non-crypto, invited DMs
  ("follow me so i can read your chats") — follow+DM PENDING (user took the tab back;
  retry when browser idle). @Njau_ "looking for a graphic designer" 1h old. @FlixMNG
  designer-search thread. $PRICE/@GetPriceAPPs follow-up STILL pending (Round 7 leftover).
  Dex-update demanders: @theinternct, @bulwarktools ($65k vol pre-grad), @Daveisgeeked,
  @nanditmehra, @kekcoinonpump (delivered, follow for response). memetuber follow-up
  (mcap $5K, alive, banner delivered Round 7). PEPPER team promised "huge news" — check
  notifications first; if they launch a website/visual push, that is our in.
- SCRIPT DEBT FIXED: helper scripts must import TOKEN from bridge.py (never paste token
  literal — redaction middleware breaks it). gen_banner.mjs now parameterized
  (size/out/promptFile); hunt.py + fetch_links.py + post_banner.py + reply_banner.py +
  process_banner.py + vlm_qa.mjs + sync_hub_r8.py = full reusable pipeline.
- USER TAB INTERFERENCE: user actively browses during sessions; pinned tabId got
  navigated by the user mid-flow (again). Keep batches small, re-open dedicated tabs
  per task, never trust "active" state.

## Round 12 (2026-10-16) - BANNER PIPELINE v2 + ANTI-TEMPLATE POSTING

- USER VERDICT on R11 Agnes banners: old z-ai banners were BETTER; new ones wrong dex
  banner size; text must be "fixed over template"; coin characters must be preserved;
  30-min auto generation must stop (manual curation instead, saves GitHub quota);
  post text must be diversified or X flags bot-template activity.
- DEX BANNER SIZE TRUTH: DexScreener CDN serves every token header at 600x200 (3:1)
  (checked via api.dexscreener.com/token-profiles/latest/v1 -> header URL stripped of
  ?width/height params). Correct master = 1920x640. Agnes default output is 1248x832
  (3:2-ish) - that was the wrong-size failure. Agnes accepts OpenAI-style size param:
  {"size":"1792x512"} returns 1568x672 (widest it goes).
- BANNER v2 = deterministic composite, ZERO per-post image-gen:
  bg_pool.py (one-shot, 10 text-free wide backgrounds via Agnes, reused forever,
  "exists, skip" topping) + compose_banner.py (Playwright 1920x640 exact):
  pooled bg w/ per-coin hue/brightness/saturation grading (seed=md5(ca)) -> shade
  gradients -> hex SVG overlay -> accent orbs -> REAL coin logo (DexScreener
  info.imageUrl; initials-medallion fallback; <30min coins usually have NO logo yet,
  logo_backfill.py scans all pairs + GT) in accent ring -> CSS 900-weight gradient
  wordmark w/ stroke+glow (letter-perfect by construction -> no VLM QA) -> pills
  (chain/age/vol/buys) -> tagline. Playwright + chromium already in env.
- Round-level anti-repetition: 10 bgs + 10 taglines shuffled to distinct assignment
  per round (fix: main() assigns _bgfile, compose() must RESPECT it - pick_bg by
  seed overrode assignment and caused same-bg collisions).
- ANTI-TEMPLATE CAPTIONS (make_captions.py): 10 structural archetypes shuffled per
  round; hooks/CTAs/emoji sampled WITHOUT replacement; 6 URL + 4 mention-only CTAs
  (all carry an order entry); weighted len<=265 counting URL=23; watch grammar on
  singular ages ("its first a minute" bug -> special-case 'a minute'/'1min').
- POSTING OPS: 10-min bash tool timeout killed the poster mid-round -> runner now
  takes slug args to RESUME (post_r12_all.py ex_r12 jeet_r12 ...). Toast "sent:
  False" twice was FALSE NEGATIVE - profile showed the post live seconds later.
  GOLDEN RULE upheld: always profile-check before retry, never double-post.
- Tab hygiene incident: user took the composer tab back mid-flow (screenshot showed
  the Z.ai chat). Sensitive flows (delete/pin menus) now run in a FRESH newTab.
- Pin menu positions on own post: pinned post caret = [Delete, Unpin, Highlight...],
  unpinned own post caret = [Delete, Edit, Pin to your profile(pos3/idx2), Highlight...].
  Delete confirm = confirmationSheetConfirm; pin toast "Your post was pinned to your
  profile."
- banner-forge de-scheduled: cron */30 removed (workflow d30806df) + README claim
  patched (d4fa2a2a). Forge = issue-driven only; Agnes Actions secret unchanged
  (never exposed). DexScreener API 429s are rising - pace calls.

## Round 15 (Oct 17, 2026)
- Tool infra outage (prod-wsmgr-svc EOF) can kill tool calls mid-round; background
  jobs (nohup/setsid) still get reaped when a Bash call times out or returns ->
  run long Agnes merges as FOREGROUND calls with timeout budget; merge_bgs skips
  cached outputs so re-invocation resumes cleanly.
- page.content action is DEAD in extension v1.1.2 (empty html even with explicit
  tabId). All X reads now via page.screenshot + fetch_bin.py + vision.
- GeckoTerminal relationship ids are COMPACT format "eth_0x.../solana_..." (no
  slash path). Strip the network prefix before calling DexScreener, else DS
  returns nothing and buys-verification silently reports 0/NO PAIR.
- Rate-limit stack seen simultaneously: DexScreener search 429, GT new_pools 429,
  pump.fun frontend 530 (cloudflare). Working combo: DS batch /tokens/{30} +
  paced GT new_pools (12s/network) + boosts/profiles. Traction filter can run on
  vol+liq alone when buys verification is unavailable.
- X composer char-limit = SILENT failure mode: over-limit shows "-N" red and the
  Post button is disabled; click returns ok but nothing posts. ALWAYS pre-count
  weighted length (URL=23) on hand-written captions before intent_post.
- QA stray_text can be a FALSE POSITIVE when the coin's original logo itself
  contains lettering (POLARBEARS "SAVE THE POLAR BEARS" chest slogan) - human
  override with eyes on the image before re-merging.
- Agnes 503 "image queue is full" storms: sequential + patient retries win;
  template wheel seed shift (seed0 % 6) picks a different scene recipe on remerge.
- AI-agent coin meta (wormcast study): entity = LLM on a wake schedule posting
  from long-term memory + coin on pump.fun + nursery launchpad (coins priced in
  the parent token = forced buy pressure). wormcast itself launched Oct 17, kill
  switch ON, nursery not active. For Eye: coin launch needs user's wallet
  (Phantom signing is manual; extension v1.1.2 has no eval and cannot approve).
  AI-agent-launched coins (clanker etc.) already flow into the existing hunt.

## Round 16 (2026-10-17) - T2I HUMAN-FIGURE INCIDENT + POST REPAIR PROTOCOL

- USER DIRECTIVE: NO $EYE coin launch for now. If user launches later, or X people
  launch a coin "for the agent", support it then. Daily routine continues as standard.
- T2I HUMAN-FIGURE INCIDENT: old t2i fallback prompt ("one heroic central subject")
  produced literal HUMANS in 6/9 logo-less banners (TRADER suited man w/ face,
  P2L/liangzibi superheroes, CBUCKS faceless caped figure, STARCOIN cosmic humanoid,
  ALT smoke-man). Agnes vision QA scored them PASS (invented_humans=False) - QA CANNOT
  be trusted for human detection. Human eyeball of every t2i banner is mandatory.
  FIX: t2i prompt now hard-bans people/humanoids/faces/bodies/statues/superheroes/
  silhouettes; subjects must be OBJECT/ANIMAL/ABSTRACT only. Re-merged 6+1, all clean.
- TICKER CURATION = also an ethics filter: "JEET" is slur-adjacent slang - swapped
  for BRE regardless of traction. Avoid posting banners for derogatory tickers.
- ATTACH FALSE NEGATIVE: intent_post "attach: False" does NOT mean the image is
  missing - TRADER landed WITH banner while flagged no-attach. Always search-verify
  (from:aikitapp) before any repair; never repost on the flag alone (dupe risk).
- GITHUB 409 RACE: rapid bridge batches can hit results-write 409 conflicts; the
  in-flight commands may silently not execute (p2l "post clicked: False" was truly
  not posted - search showed nothing - safe clean repost). Verify-by-search decides.
- CAPTION AUDIT v2: substring claim-lists miss paraphrases ("took the logo and turned
  it into", "this mascot goes hard", "a face you trust" on logo-less coins). Grep
  broad stems (logo/mascot/character/face/art team) gated on has_logo, and propagate
  has_logo cap_spec -> captions -> manifest (it silently dropped to None once).
- Search screenshots: page.screenshot intermittently 400s / search tab shows
  "Something went wrong" - retry fresh tab + scroll; results lag is seconds, not minutes.

## Round 17 (2026-10-17) - GROWTH AUDIT + REPAIR FLOWS MATURED

- USER DIRECTIVE: keep improving toward making money + growing. Actioned: growth audit
  (reach is the bottleneck: 3 followers, pinned=26 views top surface, fresh posts 3-4
  views each, zero inbound mentions/orders yet). Site claim bug FIXED (stale "auto-forges
  every 30 min" still on order page after R12 cron kill - always re-audit ALL surfaces
  after a capability changes).
- has_logo propagation bug is RECURRING (2nd round in a row): make_captions_v2 output
  drops the flag -> audit flags legit i2i claims as false (DI/Mechazilla/RIGLOOP) AND
  missed real t2i violations (GROKLET "mascot", Bicasso "character"). FIX PROPERLY
  next round: write has_logo into captions_v2.json inside make_captions_v2 itself.
- SILENT POST FAILURE mode #2: clean flags (attach True, clicked True, shot captured)
  but post NOT live (GROKLET). Post-count check (profile header) is the cheapest
  global sanity: 176 vs expected 177 exposed it. Always reconcile post count + search
  verify EVERY ticker before closing a round.
- DELETE FLOW LESSONS: caret deep.click is flaky on stale/overlay tabs (ok:False twice);
  fresh tab fixed it. Menuitem click needs div[role='menuitem']:nth-of-type(1) (first-
  child pseudo failed once). Delete confirm = confirmationSheetConfirm. After delete,
  page count drops and remaining cells shift up.
- page.content PARTIALLY WORKS now: returns ~3.2K text of TOP cells only (profile top,
  notifications). Usable as quick notif/DOM check but NOT for deep timeline scans.
- Screenshot 400 bursts come in waves; DOM reads (deep.html/page.content) are the
  fallback. Batch search sometimes shows "Something went wrong" - fresh tab + scroll.
- R17 ledger: 10/10 live (BUDDIES 2536 buys, NULLA 1935, EGGPLANT, DI, GROKLET,
  Bicasso, Mechazilla, RIGLOOP, PCAT, LARP) after 2 text-only deletes + reposts and
  1 silent-fail repost. 6/10 had logos (i2i) - best logo ratio so far.

## R21 (Oct 20) - PIPELINE v7 + STRUCTURED X READER (major)
- ROOT CAUSE of the user-visible regression ("circle badge, no logo character in bg"):
  (1) build_spec_r17.py passed logo:None for ALL merge inputs -> every coin ran t2i
  envonly; (2) a composer variant pasted flat ticker-text CIRCLES on the right.
  v7 FIX (scripts now): merge_bgs.py DELETED the pure-t2i path - every coin gets a
  logo SOURCE first: official logo if any, else make_emblem.py forges a square
  emblem (ticker-themed, no humans/text) that then runs the SAME i2i templates.
  compose_banner_v7.py has ZERO badge code + HARD GATE bg_has_logo=true (refuses
  to compose otherwise). Deterministic fallback (i2i exhausted): Agnes empty-scene +
  PIL in-scene paste - human-proof, badge-free.
- PIL PASTE TRAPS (3 bugs found by eyeball loop): (a) Image.point((v-br)**2) WRAPS
  values >255 (modulo) - distance maps must use numpy int32; (b) int16 overflows at
  255^2*3 -> sqrt NaN - always int32+; (c) a rectangular "vignette zone" paste reads
  as a pasted panel - the square patch was the VIGNETTE, not the keying. Final
  recipe: border-color-distance alpha (median of border px) + MaxFilter feather +
  bbox crop + layered ELLIPSE glow only. Production-quality result, zero Agnes calls.
- Agnes i2i CAN STILL INVENT HUMANS despite prompt bans (GBGPT mannequin twice, two
  different templates) -> eyeball gate remains MANDATORY; fallback to deterministic
  paste instead of re-rolling forever when the model keeps disobeying.
- BRIDGE ACTIONS (from extension.js source - always re-check source!): scroll is
  `{"action":"scroll","by":N|"to":"top|bottom"}` NOT page.scroll (silently no-ops ->
  byte-identical screenshots); page.html returns FIRST match of a shallow selector;
  deep.html depth>10 cutoff misses X articles - read timelines via page.html on
  '[data-testid="primaryColumn"]' (400K chars) then regex parse.
- x_read.py = NEW STANDARD X reader (exact handles, no more misread screenshots).
  First test caught a misread lead instantly (Raze40_ was actually RackzHQ).
- GitHub Contents API 409 races still happen on commands/pending.json (bridge) -
  one retry clears it. People-profile page.open can hang (twigglingtwigs_ 3x) ->
  substitute the lead, don't burn the round.
- Ethics filter: @CTribb09998 skipped (explicit bio) - brand safety before volume.
- R21 ledger: 5 coins (熊猫 201 buys, 重生之 107, SILL 95, LAPTOP 53, GBGPT 21; zero
  official logos -> 5 emblems forged, 2 i2i + 2 paste-fallback + 1 retry) + 5 people
  graphics (RackzHQ banner, cryptofusion23/ItsGoatxyz/gl0wingtaxicab/7dreamthinker
  pfps) via since:2026-10-20 searches. 10/10 posts live + search-verified. All coin
  backgrounds contain the logo character; zero circle badges anywhere.
- CAPTION HONESTY: emblem-forged coins get has_logo=false; sentence-level re-phraser
  in r21_manifest.py rewrites "mascot carried" claims to "Custom emblem forged first".

## R22 (2026-10-20, pump.fun focus round)
- PUMP.FUN HUNT PLAYBOOK (user directive: pump coins get more views): DexScreener
  search with pumpswap/pumpfun-first query list (r22_hunt.py) + dexId filter
  ("pumpswap","pumpfun") on solana + boosts/profiles + GT solana new_pools ->
  11/12 candidates were pump.fun. Verify step re-pulls each pick live (r22_verify.py)
  and drops dead/dumping ones (API -71% dumped out). Picks: aDOGymous 23k buys
  $1.4M vol, EVOLVE 15k, Twyne 12k, earth 11k, DUST 3.4k - ALL with official logos.
- Agnes 503 queue storms come in WAVES: 3 coins 503-stormed at 09:18, queue fully
  drained by 09:35 (i2i try7/try8 OK). Never settle for paste-fallback on the first
  storm - re-run merge 30-60 min later; i2i upgrade passes are cheap (cache skips).
- CONTEST ENTRY GRAPHICS: tradeify MILK "milkefy Alex" contest ($100K prop acct)
  -> retro 50s mascot COW milkman (animal, not human - respects the t2i human ban
  while nailing the brief). Meme campaigns want mascot style, not photoreal.
- SPEC-DRIVEN CLIENT BANNER (Hilton): his own post contained the full brief (white
  bg + black silhouettes) -> deterministic HTML/SVG compose, zero AI risk, exact
  match to ask. Always mine the lead's own post for the spec before generating.
- PROFILE-VOID LEADS: recon screenshots find "gray void" banners instantly
  (Woodenplank24) - vocal small degens with default banners are the easiest
  graphic gifts and they notice them.
- DUPLICATE POST TRAP: intent_post "post clicked: False" does NOT guarantee
  nothing posted (earth first attempt landed despite 409 + clicked:False) ->
  ALWAYS profile-read and reconcile post count before retrying a failed post;
  delete the dup via profile caret flow (scroll profile FIRST: X virtualizes
  off-screen cells, caret on unmounted cell = ok:False).
- BRIDGE SATURATION: ~40 page.open newTab cycles in one round eventually wedges
  the extension (page.open times out, then even screenshots die). Rest 2-5 min;
  if still dead, end browser work, finish file-side tasks (captions/audit/sync
  use GitHub API, not the bridge). Consider tab-hygiene in a future extension fix.
- R22 ledger: 5 pump.fun coin banners (3 i2i upgraded after storm, 2 deterministic
  paste; all bg_has_logo=true) + 5 people graphics (hilton_yt, milkman_cow contest,
  milk_promo, plank_cat, thumbhero). 10/10 posts LIVE on profile (profile-read
  verified). 1 earth dup pending deletion (bridge wedge).
