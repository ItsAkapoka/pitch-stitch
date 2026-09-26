# The Pitch Stitch: setup guide (Cloudflare)

This is your Pitch Stitch GPT, rebuilt as a free elevator pitch generator you own. People sign up through your Kit form, land on the Pitch Stitch, and answer seven questions while the coach reacts to each answer, just like the GPT did. Then they get their hype paragraph, two pitches (The Handshake and The Room), and your approved "next thread" with one fit call button.

**What it costs:** Cloudflare hosting is free. The only running cost is Anthropic usage, a few cents per person (the reactions between answers use a small, fast model, and the final pitch uses a stronger one). You set a monthly cap.

**What's in the folder**

- `public/index.html` is the page people see: the questions, the reactions, and the results.
- `public/logo.png` and `public/fonts/` hold your logo and fonts.
- `src/index.js` is the private piece that holds your Anthropic key and talks to Claude.
- `wrangler.jsonc` and `package.json` are settings files. Leave them as they are.

Plan on under an hour the first time. Nothing here needs coding.

---

## Step 1: Get an Anthropic API key

1. Go to console.anthropic.com and create an account.
2. Add a payment method under **Billing**.
3. Under **Limits**, set a monthly spend limit (for example $25) so a surprise traffic spike can't run up a bill.
4. Go to **API Keys**, create a key, and copy it somewhere safe.
5. While you're there, read the privacy terms so you can speak to how people's answers are handled.

## Step 2: Put the files on GitHub

1. Create a free account at github.com.
2. Create a new **private** repository called `pitch-stitch`.
3. Click **uploading an existing file** and drag in everything from this folder, keeping the `public` and `src` folders intact.

## Step 3: Publish on Cloudflare (free)

1. Create a free account at cloudflare.com.
2. In the dashboard, go to **Compute (Workers) → Workers & Pages → Create**.
3. Choose **Import a repository**, connect your GitHub account, and pick `pitch-stitch`. Keep the default settings and click **Deploy**.
4. When it finishes, you'll get a link like `pitch-stitch.yourname.workers.dev`.

## Step 4: Add your key

1. Open your `pitch-stitch` Worker and go to **Settings → Variables and Secrets**.
2. Add `ANTHROPIC_API_KEY` with your key from Step 1. Set the type to **Secret**.
3. Save and deploy, then open your link and run through the whole tool once.

## Step 5: Put it on your Squarespace site

Create a page for the tool (for example `/pitch-stitch`) and add a **Code** block with this, swapping in your real link:

```html
<iframe src="https://pitch-stitch.yourname.workers.dev" allow="microphone; clipboard-write" style="width:100%;min-height:950px;border:0;" title="The Pitch Stitch"></iframe>
```

**Keep the `allow="microphone; clipboard-write"` part.** It lets the dictation button and the copy buttons work inside your page.

**About the address:** people using it on your site won't notice the workers.dev address, since it sits inside your page. A branded address like `pitch.threadstudiocollective.com` means moving your domain settings to Cloudflare. It's free but a bigger step, so it can wait.

## Step 6: Connect your Kit form

Your Kit form collects the email, and the tool itself collects nothing.

1. In Kit, open (or create) your Pitch Stitch form and make sure it adds the **Pitch Stitch** tag, which starts your email sequence.
2. In the form's settings, set what happens after someone subscribes to **Redirect to an external page**, and paste the address of your Squarespace page from Step 5.
3. Put the form wherever you promote the Pitch Stitch: your Resources page, LinkedIn, and cafecito invites.

Now the flow is: sign up through Kit → land on the Pitch Stitch → get the pitch.

---

## Good to know

- **The reactions between answers:** after each answer, a short, specific reaction appears as the next question opens. If an answer is too thin to build a strong pitch, the coach asks one follow-up question first. It never asks more than one follow-up per question. If the AI is ever slow, the tool simply moves on.
- **Dictation:** every answer box has a "Speak your answer" button. People talk, their words appear in the box, and they can edit before continuing. It uses the browser's built-in speech-to-text, so it works in Chrome, Edge, and Safari and is hidden in browsers that don't support it (like Firefox). On phones, the keyboard's own mic works too.
- **Your next threads:** the five closing messages are yours, word for word, in `public/index.html` under `NEXT_THREADS`. The AI only chooses which one fits, so it can never say something you haven't approved.
- **Your data:** the tool doesn't save anything. Answers go to Anthropic to write the reactions and pitch. If someone uses dictation, their browser's own speech service turns their voice into text (in Chrome, that's Google). The welcome screen says the tool doesn't save answers.
- **One honest note:** since the Kit form sits in front of the tool, someone who finds the tool's direct link could skip the form. That's rare, and the spend cap and hourly limits keep it harmless.
- **Branding:** your colors are listed at the top of `index.html` under "Brand tokens." Manrope and the script font are included. Your headline font, Chunky Heart, is licensed, so Bagel Fat One stands in. If your license covers web use, add it as `public/fonts/chunky-heart.woff2` and the page switches automatically.
- **Voice rules:** the rules for the reactions and the pitch live in `src/index.js` (`REFLECT_PROMPT` and `SYSTEM_PROMPT`). Run changes there past Claude so nothing breaks.
- **Making changes:** edit a file on GitHub and Cloudflare updates the live tool within a minute or two.
- **Ready for the quiz:** a link like `.../?role=connector` pre-selects that person's tone, so your quiz can send people straight here later.
- **Abuse protection:** limits of 5 pitches and 60 reactions per person per hour, plus your Anthropic spend cap.
- **Keys stay private.** Never paste your key into `index.html`, only into Cloudflare's Secrets.
