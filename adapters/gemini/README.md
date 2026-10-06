# Gemini Apps Adapter

**Status: adapter drafted — runtime validation pending**

Gemini Apps now supports reusable Skills on eligible personal Google Accounts. Skills can be automatically applied when relevant or explicitly invoked.

## Important distinction

Gemini Apps is **not** Antigravity. Do not copy Antigravity filesystem paths or assume local-shell capabilities.

## Security gate

Before claiming the full Find Skills Pro workflow on Gemini Apps, verify whether the active Skills runtime can execute NVIDIA SkillSpector or otherwise call a trusted external scan path.

If the scanner cannot run, the adapter must stop before treating a candidate as security-cleared.

Official references:
- https://support.google.com/gemini/answer/17094296
- https://support.google.com/gemini/answer/18560919
