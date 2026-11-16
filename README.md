# Metacritic (minus Slant)

Chrome extension that removes Slant Magazine from Metacritic critic reviews and recalculates the displayed Metascore and review statistics without it.

> Independent project. Not affiliated with, endorsed by, or sponsored by Metacritic, Fandom, or Slant Magazine.

## What it does

- Removes Slant Magazine review cards from Metacritic product pages.
- Replaces the displayed label with **METASCORE (- Slant)**.
- Recalculates the visible Metascore using an estimated Slant weight of 2.5×.
- Updates Positive, Mixed, and Negative counts, percentages, and bars.
- Updates the critic-review count and All Platforms summary.
- Works on product pages and critic-review detail pages.
- Leaves the User Score and user-review statistics untouched.

The extension supports movies, TV shows, games, and music pages.

## Install from GitHub

Chrome does not allow permanent one-click installation of extensions from ordinary websites. Install this repository as an unpacked extension:

1. Download the latest release ZIP from the repository's **Releases** page.
2. Extract the ZIP to a permanent folder. Do not delete that folder afterward.
3. Open `chrome://extensions` in Chrome.
4. Enable **Developer mode**.
5. Click **Load unpacked** and select the extracted `metacritic-senza-slant` folder.
6. Open or reload a Metacritic product page.

## Updating

1. Download and extract the latest release, replacing the previous files.
2. Open `chrome://extensions` and click the extension's **Reload** button.
3. Reload any open Metacritic tabs.

## How the estimate works

Metacritic does not publish its outlet weights or internal decimal scores. The 2026 *The Legend of Zelda: Ocarina of Time* case—where a 70 from Slant moved the displayed Metascore from 96 to 95—suggests that Slant carried at least roughly 2.3 times the weight of an average review near the rounding boundary. This extension uses a conservative estimated weight of **2.5×**.

```text
(official score × estimated total weight − Slant score × 2.5)
÷ remaining estimated weight
```

The result is rounded to the nearest integer. Reviews without a numeric score remain in the overall review total but are excluded from the Metascore denominator and sentiment distribution.

This is an independent estimate, not an official Metacritic score.

## Privacy

The extension does not collect, store, sell, or transmit personal data. It only reads public Metacritic pages and requests public review data from `backend.metacritic.com` to perform calculations locally in the browser.

See [PRIVACY.md](PRIVACY.md) for the complete privacy policy.

## Permissions

- `https://www.metacritic.com/*` — identifies and updates Metacritic product pages.
- `https://backend.metacritic.com/*` — retrieves public critic-review data for recalculation.

No browsing-history, account, storage, advertising, analytics, or tracking permission is requested.

## Development

This is a Manifest V3 extension with no build step and no third-party dependencies.

```text
manifest.json   Extension configuration
background.js   Fetches reviews and calculates adjusted statistics
content.js      Updates the Metacritic interface
styles.css      Hides excluded review cards
```

Load the repository folder with **Load unpacked**, then click **Reload** on `chrome://extensions` after each change.

## Limitations

- The adjusted score is an estimate because Metacritic's weights are not public.
- Changes to Metacritic's HTML or API may require an extension update.
- Extensions installed from GitHub must be updated manually.

## License

Released under the [MIT License](LICENSE).
