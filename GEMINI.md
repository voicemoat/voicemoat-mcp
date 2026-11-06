# VoiceMoat

VoiceMoat connects your LinkedIn and Twitter accounts. Use its tools when the user asks about their posts, their voice, their analytics, or wants content drafted, checked, scheduled or published.

- Read the voice profile (`get_voice_profile`) before drafting, so drafts read like the user.
- Check a draft with `score_voice_match` before suggesting it is ready.
- Posting always asks twice: `publish_post` and `schedule_post` first return a preview and a one-time code. Show the user the exact text and account, and only send the second call after they confirm. If the text changes, get a new preview.
- Ask which account (LinkedIn or Twitter) when it is not clear. `list_profiles` shows the connected accounts.
