# Ox Alpha Privacy & Safety Checker

Ox Alpha is a free stealth model on OpenRouter with a 1M-token context window.
The provider is anonymous and retains prompts and completions. This tool helps
you decide what is safe to send it.

Static single-page tool. No build step, no dependencies.

## Facts, and where they come from

Every claim on the page is quoted from OpenRouter's own model page for
[`stealth/ox-alpha`](https://openrouter.ai/stealth/ox-alpha) and its public API,
read on 2026-08-20.

- **Provider:** anonymous third party. OpenRouter routes to it but is not the
  developer, owner, or provider.
- **Retention:** prompts and completions are retained by the provider.
- **Training:** not used for training, per OpenRouter's stated terms.
- **Context:** 1,048,576 tokens (verified via `/api/v1/models`).
- **Pricing:** $0 prompt / $0 completion, preview.

OpenRouter's exact wording:

> This stealth model is developed and operated by a third-party model provider.
> Prompts and completions for this model are retained by the provider and are not
> used for training; all other use is governed by the Stealth Model Terms.

## Scoring

Ten data types carry weights reflecting what disclosure would actually cost --
credentials (30) and customer records (28) score highest because the damage is
immediate and irreversible; public code scores 0. Weights sum, cap at 100, and
band into low (<25), medium (25-54), high (55+).

This is a judgement, not a standard.

## Funnel

The page has no product CTA. The conversion is a button to ai-tldr.dev.

It is a standing block placed after the alternatives table, not a result-gated
CTA and not an email capture. Three deliberate choices:

- **A link, not a form.** Asking for an email on a page someone landed on
  thirty seconds ago converts badly and reads as a toll gate. Send them to the
  site and let it make its own case.
- **Always present.** Visitors who never tick a box still see it, and they are
  a large share of the traffic.
- **Placed late.** After the answer and the alternatives, so it reads as the
  closing note of the dossier rather than an interruption.

The framing is what keeps the tool useful after the initial spike: this page's
own answer has an expiry date, so "track what changes" is the honest completion
of the tool rather than a bolted-on ask.

## What this deliberately does not claim

An anonymous provider is not the same as a bad actor, and stealth previews are a
normal way to test a model before launch. The page says so explicitly. The
narrower point stands: you cannot evaluate a data policy when you do not know
whose it is.

## Maintenance

Stealth models get named, free pricing ends, and terms change. Re-verify against
the source before relying on any of it:

    curl -s https://openrouter.ai/api/v1/models \
      | python3 -c "import json,sys; d=json.load(sys.stdin)['data']; \
        m=[x for x in d if x['id']=='stealth/ox-alpha'][0]; print(json.dumps(m,indent=2))"

Update the masthead date when you do.

## Deploy

    vercel --prod

Static site, framework preset **Other**, no build command, output directory `.`.

## Licence

MIT. Not affiliated with OpenRouter or the Ox Alpha provider.
