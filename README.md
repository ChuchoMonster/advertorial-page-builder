# DTC Advertorial Page Builder (a Claude Code prompt)

This repo is a `CLAUDE.md` file of about 18KB that turns Claude Code into a generator for direct-to-consumer **advertorial pages**: the editorial-looking pages that sit between a Meta ad and a product page. There's no application code. The prompt is the product.

## How it works

Open this folder in Claude Code and ask it to build an advertorial. Claude Code picks up `CLAUDE.md` automatically, and from then on it:

1. **Asks six questions at once**: brand/product/price, target customer, mechanism (the "why this works" angle), proof, a style preset, and optional product image URLs.
2. **Applies one of four style presets**, each with its own palette, type and narrator:
   - A, Clinical Editorial: medical journal / health magazine
   - B, Lifestyle Magazine: polished feature article
   - C, News Exposé: consumer-investigation tone
   - D, Warm & Trustworthy: a recommendation from a friend
3. **Builds a fixed 17-section structure** in a fixed order: urgency banner, editorial headline, byline, hero image, opening hook, star-rating break, pain-point escalation, root-cause reframe, product reveal, ingredient/feature cards, testimonials, results timeline, comparison table, three-tier pricing, guarantee, final CTA, footer.
4. **Generates images** through the kie.ai API (Nano Banana 2) if no product images were supplied. The prompt includes the endpoints, polling flow, error codes and per-preset image-prompt guidance.
5. **Outputs a single self-contained `index.html`**: inline CSS, Google Fonts only, no JavaScript, mobile-first, with ≥48px tap targets.

The prompt also sets copy rules: write like a journalist rather than a marketer, prefer specific numbers, keep one idea per paragraph, never use a list of banned "AI vocabulary" words, and make testimonials sound like real people.

## Example

`examples/sample-page.html` is a short, hand-written sample laid out the way the prompt specifies. It uses preset B and a **fictional** cold-brew brand, "Lumen Brew". The brand, editor, reviews, ratings and prices are all invented and labelled as such on the page. Images are CSS-gradient placeholders, so the page loads no external images. Open it directly in a browser.

## What's AI-generated vs hand-written

- `CLAUDE.md`: written by John Freund (with AI assistance), based on the structure of advertorials running on Meta.
- Pages it produces: written and coded by Claude at run time. Images, if generated, come from kie.ai.
- `examples/sample-page.html`: a hand-written illustration of the output format, not a real generated run.

## Setup

```bash
cp .env.example .env    # add your kie.ai key (only needed for image generation)
claude                  # start Claude Code in this folder, then: "build an advertorial"
```

## Environment variables

| Name | Used for | Required? |
|---|---|---|
| `KIE_API_KEY` | kie.ai image/video generation, called by Claude Code from the prompt's API recipe | Only if you want generated images |

## Responsible use

Advertorials are regulated advertising. In the US, the FTC's endorsement and native-advertising rules apply. If you use this prompt on a real product, the page must be clearly labelled as an advertisement, testimonials must come from real customers whose results are typical (or be disclosed), and expert bylines and credentials must be real.
